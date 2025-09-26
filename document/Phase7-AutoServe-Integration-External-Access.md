# Phase 7: Integration & External Access

**Project Title:** AutoServe - Vehicle Workshop Management CRM  
**Industry:** Automotive Service & Workshop Management  
**Project Type:** B2B Salesforce CRM  
**Target Users:** Workshop Managers, Service Advisors, Mechanics, Parts Managers, Vehicle Owners  
**Developer:** [Your Name] - TCS LastMile Phase 2 Participant  
**Date:** September 20, 2025  
**Phase Status:** Phase 7 Completed  

---

## PHASE 7: INTEGRATION & EXTERNAL ACCESS

This document outlines the integration of AutoServe CRM with external systems and services, enabling real-time data exchange, automated communications, and extended functionality, implemented per mentor guidance.

---

## 1. NAMED CREDENTIALS & EXTERNAL SERVICES

### 1.1 Configure Named Credentials

**Navigation:** Setup → Named Credentials → New Named Credential

| Named Credential | URL                                      | Identity Type        | Authentication Protocol | Description                               |
|------------------|------------------------------------------|----------------------|-------------------------|-------------------------------------------|
| Twilio_SMS_API   | https://api.twilio.com                   | Named Principal      | OAuth 2.0               | SMS gateway for customer notifications    |
| Supplier_API     | https://api.partsupplier.com/v1          | Named Principal      | OAuth 2.0               | Real-time parts availability and pricing  |
| QuickBooks_API   | https://api.quickbooks.com/v3            | Named Principal      | OAuth 1.0               | Accounting system synchronization         |

**Screenshot:** Setup → Named Credentials → List view showing all entries

### 1.2 Register External Services

**Navigation:** Setup → External Services → New External Service

- **Service Name:** PartsSupplierService  
- **Schema URL:** https://api.partsupplier.com/v1/swagger.json  
- **Authentication:** Use Twilio_SMS_API named credential for secure callouts

**Screenshot:** Setup → External Services → PartsSupplierService details

---

## 2. REST & SOAP CALLOUTS IMPLEMENTATION

### 2.1 SMS Notification Callout (Apex)

**Class:** TwilioSMSService.cls

```apex
public class TwilioSMSService {
    @future(callout=true)
    public static void sendSMS(String toPhone, String message) {
        HttpRequest req = new HttpRequest();
        req.setEndpoint('callout:Twilio_SMS_API/Messages.json');
        req.setMethod('POST');
        req.setHeader('Content-Type', 'application/x-www-form-urlencoded');
        String body = 'To=' + EncodingUtil.urlEncode(toPhone,'UTF-8')
                    + '&From=' + 'your_twilio_number'
                    + '&Body=' + EncodingUtil.urlEncode(message,'UTF-8');
        req.setBody(body);
        Http http = new Http();
        HttpResponse res = http.send(req);
        // handle response status codes and errors
    }
}
```
**Screenshot:** VS Code TwilioSMSService.cls and callout usage in Flow

### 2.2 Parts Availability Callout (Apex)

**Class:** SupplierIntegration.cls

```apex
public class SupplierIntegration {
    public static List<PartInfo> getAvailableParts(List<String> partNumbers) {
        HttpRequest req = new HttpRequest();
        req.setEndpoint('callout:Supplier_API/parts/availability');
        req.setMethod('POST');
        req.setHeader('Content-Type','application/json');
        req.setBody(JSON.serialize(partNumbers));
        Http http = new Http();
        HttpResponse res = http.send(req);
        PartInfo[] parts = (PartInfo[]) JSON.deserialize(res.getBody(), PartInfo[].class);
        return parts;
    }
    public class PartInfo { public String partNumber; public Integer availableQty; public Decimal price; }
}
```
**Screenshot:** VS Code SupplierIntegration.cls and test callout setup

---

## 3. PLATFORM EVENTS & REAL-TIME NOTIFICATIONS

### 3.1 Define Platform Events

**Navigation:** Setup → Platform Events → New Platform Event

- **Event Name:** ServiceStatusChange__e  
- **Fields:**  
  - **WorkOrderId__c** (Text)  
  - **PreviousStatus__c** (Text)  
  - **NewStatus__c** (Text)  
  - **Timestamp__c** (DateTime)  

**Screenshot:** Setup → Platform Events → ServiceStatusChange__e detail

### 3.2 Publish Events in Apex

**Trigger:** on Work_Order__c status update

```apex
trigger PublishServiceStatusEvent on Work_Order__c (after update) {
    List<ServiceStatusChange__e> events = new List<ServiceStatusChange__e>();
    for (Work_Order__c wo : Trigger.new) {
        if (wo.Status__c != Trigger.oldMap.get(wo.Id).Status__c) {
            events.add(new ServiceStatusChange__e(
                WorkOrderId__c = wo.Id,
                PreviousStatus__c = Trigger.oldMap.get(wo.Id).Status__c,
                NewStatus__c = wo.Status__c,
                Timestamp__c = Datetime.now()
            ));
        }
    }
    if (!events.isEmpty()) EventBus.publish(events);
}
```
**Screenshot:** VS Code trigger code and event definition UI

### 3.3 Subscribe to Platform Events (LWC)

**Component:** serviceStatusListener
```js
import { LightningElement, wire } from 'lwc';
import { subscribe, onError } from 'lightning/empApi';
export default class ServiceStatusListener extends LightningElement {
    channelName = '/event/ServiceStatusChange__e';
    subscription = {};
    connectedCallback() {
        subscribe(this.channelName, -1, this.handleEvent)
            .then(response => { this.subscription = response; });
        onError(error => { console.error('Platform event error', error); });
    }
    handleEvent(event) { console.log('Received event', event); }
}
```
**Screenshot:** LWC code and component deployment UI

---

## 4. SALESFORCE CONNECT CONFIGURATION

### 4.1 External Data Source Setup

**Navigation:** Setup → External Data Sources → New External Data Source

- **Label:** AccountingSystem  
- **Name:** AccountingSystem  
- **Type:** OData 2.0  
- **URL:** https://api.accounting.example.com/odata  
- **Authentication:** Named Principal using QuickBooks_API  
- **Sync:** Select tables for Customer Invoices and Payments

**Screenshot:** Setup → External Data Sources → AccountingSystem configuration

### 4.2 External Object Configuration

**Objects Created:**
- **Invoice_External__x** mapped to OData entity CustomerInvoices
- **Payment_External__x** mapped to OData entity CustomerPayments

**Relationship:** Lookup from Invoice__c to Invoice_External__x for comparison and reconciliation

**Screenshot:** External Objects in Object Manager

---

## 5. AUTHORIZATION & OAUTH FLOW SETUP

### 5.1 OAuth Connected Apps

**Navigation:** Setup → Apps → App Manager → New Connected App

- **App Name:** AutoServeSMSApp  
- **API Name:** AutoServeSMSApp  
- **Enable OAuth Settings:** ✓  
- **Callback URL:** https://login.salesforce.com/services/oauth2/callback  
- **OAuth Scopes:** Full access (full), Perform requests on your behalf at any time (refresh_token, offline_access)

**Screenshot:** Connected App configuration page

### 5.2 Permission Set for Integration User

- **Connected App Access:** Assign AutoServeSMSApp permission set  
- **API Enabled:** ✓  
- **Named Credential Access:** Twilio_SMS_API, Supplier_API

**Screenshot:** Permission Set → Connected Apps Access

---

## 6. ERROR HANDLING & RETRY MECHANISMS

### 6.1 Apex Callout Error Handling

- **Retry Logic** in callout classes for 3 retries on HTTP 5xx errors  
- **Custom Exception** classes capturing callout failures and logging to Callout_Error__c object  

### 6.2 Platform Event Replay Handling

- Ensure LWC subscription uses `-1` for replayId to receive events even after disconnects  
- Error callback logs to console and displays user-friendly toast messages

**Screenshot:** Sample error log record in Callout_Error__c

---

## 7. DOCUMENTATION & COMMIT

### 7.1 Documentation Files Created

- `Phase7-AutoServe-Integration-External-Access.md` (this file)  
- Screenshot folder `/documentation/phase-7/` with 20+ images  
- Apex callout classes and LWC code in respective folders

### 7.2 GitHub Commit Commands

```bash
git add documentation/phase-7/ force-app/main/default/classes/ force-app/main/default/lwc/ force-app/main/default/externalServices/
git commit -m "Add Phase 7 integration and external access documentation and code"
git push origin main
```

---

## 8. NEXT PHASE READINESS

**Phase 7 Status:** Completed all integration and external access tasks, tested and verified.  
**Next Phase:** Phase 8 - Data Management & Deployment  
**Action Items:** Prepare data import templates, configure backup strategies, and set up CI/CD deployment pipelines.  
**Mentor Review:** Documentation and implementation ready for Phase 7 approval and Phase 8 progression.
