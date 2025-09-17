# Phase 2: Org Setup & Configuration

## Overview
This phase covers the setup and configuration of your Salesforce org to support the EventEase CRM solution. Proper settings ensure accurate business operations, secure and role-based access controls, and a solid foundation for further development.

---

## 1. Salesforce Edition Selection
- Use Developer Edition for development and testing.
- Use Enterprise Edition or higher for production to support advanced features like workflow automation, API integrations, and more.

---

## 2. Company Profile Setup
Navigate to **Setup > Company Settings > Company Information**  
Update the following:
- Company Name: EventEase Solutions Inc.  
- Default Time Zone: Eastern Standard Time (or replace with your timezone)
- Locale & Language: English (United States)  
- Default Currency: USD  
- Fiscal Year: January to December  
- Save your changes.

---

## 3. User Licensing & Profiles
Navigate to **Setup > Users > Profiles**  
- Clone standard profiles to create:
  - Event Manager Profile
  - Finance Team Profile
  - Vendor Community Profile (Community license)
  - Client Community Profile (Community license)  
- Configure object and field permissions according to user roles:
  - Event Manager: Full CRUD on Event, Booking, Vendor, Client objects
  - Finance Team: Full access to Invoice and Payment objects
  - Vendors: Access limited to their assignments  
  - Clients: Access limited to their own events and invoices  
- Save and document each profile configuration.

---

## 4. Role Hierarchy
Navigate to **Setup > Roles > Set Up Roles**  
Configure roles:  
- CEO  
- Event Operations Manager  
- Senior Event Manager  
- Venue Coordinator  
- Finance Director  
- Finance Manager  
Assign users to relevant roles accordingly.

---

## 5. Permission Sets
Navigate to **Setup > Permission Sets**  
- Create permission sets for additional permissions like API access, data export.
- Assign permission sets to users who need extended privileges beyond profiles.

---

## 6. Organization-Wide Defaults (OWD) & Sharing Rules
Navigate to **Setup > Security > Sharing Settings**  
- Set OWD:  
  - Event, Booking, Invoice, Payment objects → Private  
  - Venue and Client objects → Public Read/Write  
- Create sharing rules:  
  - Share EventVendor junction records with assigned Vendors only  
  - Share Event records with Finance roles accordingly  
- Test sharing settings using “Login As” feature to verify access levels.

---

## 7. Field-Level Security
For each profile, configure field-level security to restrict sensitive financial and client data.  
- Finance related fields only visible to Finance profiles  
- Client data limited to assigned event managers  
- Vendors see only relevant assignment fields

---

## 8. Sandboxes
In Production org navigate to **Setup > Sandboxes**  
- Create Developer Sandbox for development and unit testing.  
- Create Partial Copy Sandbox with sample data for integration and user acceptance testing.  
- Schedule sandbox refreshes before major deployments.

---

## Documentation
Produce a detailed Phase 2 document (`Phase-2-OrgSetup.md`) including:  
- Company profile screenshots and configs  
- User license and profile setup details  
- Role hierarchy chart and descriptions  
- OWD and sharing rule configurations with screenshots  
- Permission sets details  
- Sandbox types and usage policy  
Save screenshots in a `documentation` folder.

---

## Summary Table: Phase 2 Setup Components

| Component          | Purpose                              | Business Impact                        |
|--------------------|------------------------------------|-------------------------------------|
| Company Profile    | Locale, currency, fiscal settings    | Ensures accurate date, currency, and report context  |
| User Licenses      | Controls access to CRM features       | Proper licensing avoids feature lockout and compliance |
| Profiles & Roles   | Define permissions and data visibility | Granular security and operational clarity            |
| OWD & Sharing Rules| Enforce data access policies          | Protects data privacy and ensures collaboration enforcement |
| Permission Sets    | Extend user capabilities               | Flexibility without profile overload                   |
| Sandboxes          | Safe development and testing          | Protect production data and enable iterative development  |

---

### Next Steps:
After completing Phase 2 setup and documentation, seek mentor approval before progressing to Phase 3 (Data Modeling & Relationships).

---

*This markdown document ensures comprehensive and professional Phase 2 delivery aligned to mentor expectations.*
