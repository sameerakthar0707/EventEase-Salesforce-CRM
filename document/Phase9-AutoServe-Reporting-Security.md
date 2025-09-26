# Phase 9: Reporting, Dashboards & Security Review

**Project Title:** AutoServe - Vehicle Workshop Management CRM  
**Industry:** Automotive Service & Workshop Management  
**Project Type:** B2B Salesforce CRM  
**Target Users:** Workshop Managers, Service Advisors, Mechanics, Parts Managers, Vehicle Owners  
**Developer:** [Your Name] - TCS LastMile Phase 2 Participant  
**Date:** September 20, 2025  
**Phase Status:** Phase 9 Completed  

---

## PHASE 9: REPORTING, DASHBOARDS & SECURITY REVIEW

This document outlines the creation of key reports, dynamic dashboards, and a comprehensive security review, following mentor-approved formats and leveraging Phase 1 business requirements.

---

## 1. CUSTOM REPORTS CREATED

### 1.1 Service Revenue by Service Type

**Report Type:** Work Orders with Service Type and Total Amount  
**Format:** Summary report grouped by Service_Type__c  
**Columns:** Service Type, Count of Work Orders, Sum of Total_Amount__c, Average Service Duration  
**Filters:** Service Date in current fiscal year, Status = Completed  
**Chart:** Horizontal bar chart showing revenue by service type  
**Schedule:** Monthly email to Workshop Manager  

**Screenshot:** Reports → New Report → Work Orders report configuration

### 1.2 Work Order Turnaround Time Analysis

**Report Type:** Work Orders with Scheduled Date and Completion Date  
**Format:** Matrix report grouped by Month and Status  
**Columns:** Work Order No, Scheduled Date, Completion Date, Turnaround Days (formula field)  
**Filters:** Service Date last 90 days  
**Chart:** Line chart trend of average turnaround days per month  

**Screenshot:** Reports → New Report → Turnaround analysis configuration

### 1.3 Inventory Utilization Report

**Report Type:** Inventory with Spare Part lookup and Quantity fields  
**Format:** Tabular report sorted by Quantity_Available__c ascending  
**Columns:** Spare Part Name, Part Number, Quantity Available, Reorder Level  
**Filters:** Quantity_Available less than Reorder Level  
**Conditional Formatting:** Highlight quantities in red below reorder level  

**Screenshot:** Reports → New Report → Inventory utilization configuration

---

## 2. DASHBOARDS BUILT

### 2.1 Workshop Manager Dashboard

**Components:**
1. **Revenue by Service Type** (Horizontal Bar)  
2. **Turnaround Time Trend** (Line Chart)  
3. **Critical Work Orders** (Table with conditional highlighting for emergency priority)  
4. **Inventory Status** (Donut chart showing in-stock vs. low-stock parts)  
5. **Service Appointment Pipeline** (Gauge component showing scheduled vs. capacity)  

**Filters:** Fiscal Year, Service Advisor  
**Sharing:** Public Dashboard with running user “System Administrator”  

**Screenshot:** Dashboards → New Dashboard → Workshop Manager

### 2.2 Service Advisor Dashboard

**Components:**
1. **My Open Work Orders** (List)  
2. **Overdue Appointments** (Table)  
3. **Top 5 Frequent Customers** (Bar Chart)  
4. **Upcoming Appointments Calendar** (Custom calendar component)  

**Filters:** Running user “Service Advisor”  

**Screenshot:** Dashboards → Service Advisor Dashboard config

### 2.3 Inventory & Procurement Dashboard

**Components:**
1. **Low Stock Parts** (Table)  
2. **Vendor Performance Score** (Gauge)  
3. **Monthly Parts Expenditure** (Line Chart)  
4. **Pending Purchase Orders** (List)  

**Filters:** Parts Manager role filter  

**Screenshot:** Dashboards → Inventory Dashboard config

---

## 3. SECURITY REVIEW

### 3.1 Profiles & Permission Sets Audit

**Navigation:** Setup → Profiles / Permission Sets

- Verified object and field-level permissions match stakeholder needs  
- Ensured no profile has excessive CRUD rights  
- Confirmed permission sets only grant necessary additional access  

**Screenshot:** Profiles → [Profile Name] → Object Settings review

### 3.2 Field-Level Security Validation

**Navigation:** Setup → Object Manager → [Object] → Fields & Relationships → Set Field-Level Security

- **Sensitive Fields:** Total_Amount__c, Unit_Price__c, Customer Contact details restricted appropriately  
- **Audit:** Verified each profile’s field access aligns with access matrix  

**Screenshot:** Field-Level Security settings for Invoice object

### 3.3 Sharing Settings Verification

**Navigation:** Setup → Sharing Settings

- Confirmed OWD configurations from Phase 2  
- Reviewed sharing rules for Work Orders, Inventory, Accounts  
- Validated role hierarchy data visibility through “Login As” testing  

**Screenshot:** Sharing Settings → Work Order sharing rules

### 3.4 Audit Trail and Login History

**Navigation:** Setup → View Setup Audit Trail / Login History

- **Audit Trail:** Enabled field history tracking on key objects (Work Order, Inventory, Vehicle)  
- **Login History:** Monitored for failed login attempts and suspicious activity  
- **Compliance:** Confirmed data retention period meets company policy  

**Screenshot:** Setup Audit Trail logs

---

## 4. DATA SECURITY & COMPLIANCE

### 4.1 Encryption & Shield Settings

- Confirmed encryption at rest for sensitive fields using Platform Encryption (if enabled)  
- Verified Shield Platform Events for secure audit logs  

### 4.2 Two-Factor Authentication Enforcement

**Navigation:** Setup → Session Settings → Two-Factor Authentication

- Enabled for all profiles except vehicle owners  
- Verified SMS and Authenticator app delivery  

**Screenshot:** Two-Factor settings page

---

## 5. MOBILE SECURITY CONSIDERATIONS

- Reviewed Salesforce mobile app security policies  
- Confirmed offline encryption settings and remote wipe capability  

**Screenshot:** Mobile Administration → Connected Apps and policies

---

## 6. PHASE 9 VERIFICATION

### Reports & Dashboards Validation

- Verified all reports return expected data with correct filters and groupings  
- Ensured dashboards refresh correctly and component filters work as designed  
- Confirmed running user settings display appropriate data

### Security Review Validation

- Completed role-based testing via “Login As”  
- Verified field-level and object-level security across profiles  
- Ensured no unauthorized access to sensitive customer or financial data

---

## 7. NEXT PHASE PREPARATION

**Phase 9 Status:** Completed reports, dashboards, and security review as per mentor instruction.  
**Next Phase:** Phase 10 - Final Presentation & Demo Day  
**Action Items:** Prepare executive presentations, demo scripts, user training materials, and project handoff documentation.  
**Google Form Update:** Mark "Phase 9 Completed"  
**GitHub Repo:** Push `Phase9-AutoServe-Reporting-Security.md` with related assets  

---

**Appendix:** List of report charts, dashboard component snapshots, security audit logs
