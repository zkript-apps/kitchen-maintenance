# Business Requirements Document (BRD)

## Snow Kitchen Equipment Maintenance Management System

**Version:** 1.0  
**Date:** January 29, 2026  
**Client:** Snow Kitchen Equipment Maintenance  
**Location:** Abu Dhabi, UAE

---

## 1. Executive Summary

Snow Kitchen Equipment Maintenance, located in Abu Dhabi, UAE, provides commercial kitchen equipment installation, repair, and preventive maintenance services for restaurants, hotels, schools, and hospitals across the United Arab Emirates. 

This document outlines the business requirements for a comprehensive maintenance management application that will streamline operations for two primary client types:
1. **Annual Maintenance Contract (AMC) Clients** - Scheduled preventive maintenance
2. **On-Call Maintenance Clients** - Reactive/breakdown maintenance services

The system will automate service scheduling, enable multi-channel customer communication via chatbot integration, and provide comprehensive administrative analytics.

---

## 2. Business Objectives

### 2.1 Primary Objectives
- Automate notification system for upcoming annual maintenance services
- Centralize customer inquiries from multiple messaging platforms (WhatsApp, Viber, Telegram)
- Enable efficient technician assignment and dispatch
- Provide real-time analytics and reporting for business insights

### 2.2 Success Metrics
- Reduce missed maintenance schedules by 95%
- Decrease response time to customer inquiries by 50%
- Improve technician utilization rate by 30%
- Achieve 100% visibility of daily operations through analytics dashboard

---

## 3. Stakeholders

| Stakeholder | Role | Responsibilities |
|-------------|------|------------------|
| Admin/Management | System Administrator | Full system access, analytics, user management |
| Operations Manager | Dispatcher | Assign technicians, monitor service requests |
| Technicians | Field Service | Execute maintenance tasks, update job status |
| Clients | End Users | Submit inquiries, receive notifications |

---

## 4. Scope

### 4.1 In Scope
- Client management (AMC and On-Call clients)
- Service scheduling and notification system
- Multi-platform chatbot integration (WhatsApp, Viber, Telegram)
- Technician management and assignment
- Admin dashboard with analytics
- Service history and reporting

### 4.2 Out of Scope
- Inventory/spare parts management (Phase 2)
- Financial/invoicing module (Phase 2)
- Mobile app for technicians (Phase 2)
- Integration with accounting software (Phase 2)

---

## 5. Functional Requirements

### 5.1 Client Management Module

#### FR-5.1.1 Client Registration
- System shall allow registration of two client types:
  - **Annual Maintenance Contract (AMC) Clients**
  - **On-Call Maintenance Clients**
- Required client information:
  - Business name
  - Contact person name
  - Phone number(s)
  - Email address
  - Physical address/location
  - Preferred messaging platform (WhatsApp/Viber/Telegram)
  - Client type (AMC/On-Call)
  - Contract start date (for AMC)
  - Contract end date (for AMC)
  - Service frequency (for AMC)

#### FR-5.1.2 Equipment Registry
- System shall maintain a list of kitchen equipment per client
- Equipment details:
  - Equipment type (e.g., Freezer, Chiller, Burner, Grill, Bain Marie, Kitchen Hood)
  - Brand/Manufacturer
  - Model number
  - Serial number
  - Installation date
  - Last service date
  - Next scheduled service date (for AMC)
  - Equipment status (Active/Inactive/Under Repair)

---

### 5.2 Annual Maintenance Contract (AMC) Module

#### FR-5.2.1 Service Scheduling
- System shall automatically calculate next service dates based on:
  - Contract terms
  - Service frequency (monthly, quarterly, semi-annually, annually)
  - Equipment-specific maintenance schedules

#### FR-5.2.2 Notification System
- System shall send automated notifications for upcoming services:
  - **30 days before** - Initial reminder to admin
  - **14 days before** - Follow-up reminder to admin + notification to client
  - **7 days before** - Urgent reminder to admin + confirmation request to client
  - **1 day before** - Final reminder to all parties
- Notification channels:
  - In-app notifications (Admin dashboard)
  - SMS notifications
  - Email notifications
  - WhatsApp/Viber/Telegram messages (to clients)

#### FR-5.2.3 Service Calendar
- System shall display a calendar view showing:
  - All scheduled maintenance visits
  - Technician availability
  - Overdue services (highlighted)
  - Completed services

---

### 5.3 On-Call Maintenance Module

#### FR-5.3.1 Service Request Creation
- System shall create service requests from:
  - Chatbot inquiries (automatic)
  - Manual entry by admin/operations
  - Direct client calls (logged manually)

#### FR-5.3.2 Service Request Information
- Request ID (auto-generated)
- Client information
- Equipment affected
- Problem description
- Priority level (Critical/High/Medium/Low)
- Request date/time
- Preferred service date/time
- Assigned technician
- Status (New/Assigned/In Progress/Completed/Cancelled)

#### FR-5.3.3 Priority Classification
| Priority | Description | Response Time |
|----------|-------------|---------------|
| Critical | Equipment failure affecting operations | Within 4 hours |
| High | Major malfunction, partial operation | Within 8 hours |
| Medium | Minor issues, equipment functional | Within 24 hours |
| Low | Routine requests, non-urgent | Within 48 hours |

---

### 5.4 Chatbot Integration Module

#### FR-5.4.1 Supported Platforms
- WhatsApp Business API
- Viber Business Messages
- Telegram Bot API

#### FR-5.4.2 Chatbot Capabilities
- **Greeting & Identification**
  - Welcome message
  - Client identification (by phone number)
  - New client registration flow

- **Inquiry Types**
  - Report equipment breakdown
  - Schedule maintenance visit
  - Check service status
  - Request quote
  - General inquiries
  - Emergency support

- **Conversation Flow**
  ```
  1. Client initiates chat
  2. Bot greets and asks for inquiry type
  3. Bot collects relevant information:
     - Equipment type
     - Problem description
     - Urgency level
     - Preferred contact time
  4. Bot confirms details and creates service request
  5. Bot notifies Snow Kitchen team
  6. System assigns to appropriate personnel
  7. Client receives confirmation with request ID
  ```

#### FR-5.4.3 Handoff to Human Agent
- System shall allow seamless handoff from chatbot to human operator when:
  - Client requests to speak with a person
  - Bot cannot understand the inquiry after 2 attempts
  - Complex technical questions arise
  - Emergency situations

#### FR-5.4.4 Notification to Snow Kitchen Team
- Real-time notifications when:
  - New inquiry received
  - High/Critical priority request submitted
  - Client waiting for response > 5 minutes
- Notification includes:
  - Client name and contact
  - Inquiry summary
  - Priority level
  - Platform used (WhatsApp/Viber/Telegram)

---

### 5.5 Technician Management Module

#### FR-5.5.1 Technician Profile
- Employee ID
- Full name
- Contact information
- Specializations (e.g., Refrigeration, Gas Equipment, Electrical)
- Certifications
- Availability status (Available/On Job/Off Duty/Leave)
- Current location (optional GPS integration)

#### FR-5.5.2 Job Assignment
- System shall allow assignment of service requests to technicians based on:
  - Technician availability
  - Specialization match
  - Geographic proximity (optional)
  - Current workload
- Assignment can be:
  - Manual (by operations manager)
  - Semi-automatic (system suggests, human confirms)

#### FR-5.5.3 Job Status Updates
- Technicians can update job status:
  - En Route
  - Arrived
  - Work Started
  - Work Completed
  - Parts Required (job paused)
- Status updates trigger notifications to:
  - Admin dashboard
  - Client (via preferred channel)

---

### 5.6 Admin Dashboard & Analytics Module

#### FR-5.6.1 Dashboard Overview
- Real-time metrics display:
  - Total active clients (AMC vs On-Call)
  - Open service requests
  - Completed jobs (today/week/month)
  - Technician availability
  - Pending assignments
  - Overdue maintenance alerts

#### FR-5.6.2 Analytics & Reports

**Daily Analytics:**
- Jobs completed today
- New service requests
- Active chatbot conversations
- Response time metrics
- Technician performance

**Weekly/Monthly Analytics:**
- Service request trends
- Client acquisition/retention
- Equipment failure patterns
- Revenue by service type (if integrated)
- Technician utilization rates

**Charts & Visualizations:**
- Line charts: Service requests over time
- Bar charts: Jobs by equipment type
- Pie charts: Request priority distribution
- Heat maps: Busy days/hours
- Geographic maps: Client locations

#### FR-5.6.3 Filtering Capabilities
- Filter by:
  - Date range (custom)
  - Client type (AMC/On-Call)
  - Client name/ID
  - Equipment type
  - Service status
  - Technician
  - Priority level
  - Platform (WhatsApp/Viber/Telegram)
  - Location/Area

#### FR-5.6.4 Report Generation
- Export reports in:
  - PDF format
  - Excel/CSV format
- Scheduled reports (daily/weekly/monthly email)

---

### 5.7 User Management Module

#### FR-5.7.1 User Roles & Permissions

| Permission | Admin | Operations Manager | Technician |
|------------|-------|-------------------|------------|
| View Dashboard | ✓ | ✓ (Limited) | ✗ |
| View Analytics | ✓ | ✓ (Limited) | ✗ |
| Manage Clients | ✓ | ✓ | View Only |
| Manage Technicians | ✓ | View Only | ✗ |
| Assign Jobs | ✓ | ✓ | ✗ |
| Update Job Status | ✓ | ✓ | ✓ (Own jobs) |
| View Chatbot Conversations | ✓ | ✓ | ✗ |
| Respond to Chats | ✓ | ✓ | ✗ |
| System Settings | ✓ | ✗ | ✗ |
| User Management | ✓ | ✗ | ✗ |

---

## 6. Non-Functional Requirements

### 6.1 Performance
- Page load time: < 3 seconds
- Chatbot response time: < 2 seconds
- Support minimum 100 concurrent users
- Real-time notification delivery: < 5 seconds

### 6.2 Availability
- System uptime: 99.5%
- 24/7 chatbot availability
- Scheduled maintenance window: 2-4 AM UAE time

### 6.3 Security
- SSL/TLS encryption for all data transmission
- Role-based access control (RBAC)
- Password policy enforcement
- Session timeout after 30 minutes of inactivity
- Audit logs for all critical actions
- GDPR/UAE data protection compliance

### 6.4 Scalability
- Support growth to 500+ clients
- Support 10+ concurrent technicians
- Handle 1000+ monthly service requests

### 6.5 Usability
- Responsive design (desktop, tablet, mobile)
- Arabic and English language support
- Intuitive navigation
- Accessibility compliance (WCAG 2.1 AA)

---

## 7. Integration Requirements

### 7.1 Messaging Platform APIs
| Platform | Integration Type | Purpose |
|----------|-----------------|---------|
| WhatsApp | Business API | Chatbot + Notifications |
| Viber | Business Messages API | Chatbot + Notifications |
| Telegram | Bot API | Chatbot + Notifications |

### 7.2 Notification Services
- SMS Gateway (for SMS notifications)
- Email Service Provider (SMTP/API)
- Push notification service (for future mobile app)

### 7.3 Future Integrations (Phase 2)
- Google Maps API (technician routing)
- Accounting software (QuickBooks/Zoho)
- Inventory management system

---

## 8. Data Requirements

### 8.1 Data Entities
- Clients
- Equipment
- Service Requests
- Maintenance Schedules
- Technicians
- Users
- Chat Conversations
- Notifications
- Audit Logs

### 8.2 Data Retention
- Active client data: Indefinite
- Service history: Minimum 5 years
- Chat conversations: 2 years
- Audit logs: 3 years

### 8.3 Backup & Recovery
- Daily automated backups
- Point-in-time recovery capability
- Maximum data loss tolerance: 1 hour
- Recovery time objective: 4 hours

---

## 9. User Stories

### 9.1 AMC Client Notifications
> **As an** Admin  
> **I want to** receive automated notifications for upcoming annual maintenance services  
> **So that** I can proactively schedule technician visits and never miss a service date

### 9.2 Chatbot Service Request
> **As a** Restaurant Owner (Client)  
> **I want to** report equipment issues via WhatsApp  
> **So that** I can quickly get help without making phone calls during busy hours

### 9.3 Technician Assignment
> **As an** Operations Manager  
> **I want to** assign service requests to available technicians  
> **So that** issues are resolved quickly by the right person

### 9.4 Analytics Dashboard
> **As an** Admin  
> **I want to** view daily/weekly/monthly analytics with filters  
> **So that** I can make data-driven business decisions

### 9.5 Real-time Updates
> **As a** Client  
> **I want to** receive updates when a technician is on the way  
> **So that** I can prepare for their arrival

---

## 10. Assumptions

1. Snow Kitchen has or will obtain WhatsApp Business API access
2. Clients have smartphones with messaging apps installed
3. Technicians have access to devices for status updates
4. Reliable internet connectivity is available
5. Client database can be migrated from existing records

---

## 11. Constraints

1. Budget limitations may affect feature prioritization
2. WhatsApp Business API requires Facebook Business verification
3. Telegram and Viber have API rate limits
4. UAE data residency requirements may apply

---

## 12. Risks & Mitigation

| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|------------|
| Messaging API changes | High | Medium | Implement abstraction layer for easy platform switching |
| Low client adoption of chatbot | Medium | Medium | Provide training and incentives; maintain phone support |
| Data security breach | High | Low | Implement robust security measures, regular audits |
| System downtime | High | Low | Cloud hosting with redundancy, 24/7 monitoring |

---

## 13. Glossary

| Term | Definition |
|------|------------|
| AMC | Annual Maintenance Contract |
| On-Call | Reactive maintenance service without contract |
| Service Request | A logged request for maintenance or repair |
| Technician | Field service engineer who performs repairs |
| Chatbot | Automated messaging system for customer interaction |
| Dashboard | Visual interface displaying key metrics and data |

---

## 14. Approval

| Role | Name | Signature | Date |
|------|------|-----------|------|
| Project Sponsor | | | |
| Business Owner | | | |
| Technical Lead | | | |

---

## Appendix A: Equipment Categories

Based on Snow Kitchen's product range:
- Bain Marie
- Burners & Grills
- Freezers, Chillers & Showcases
- Kitchen Hoods
- Shelving & Racking
- Sinks
- Trolleys
- Work Tables & Cupboards
- Cold Rooms
- Bakery Equipment
- Exhaust Systems
- Gas Cookers
- HVAC Systems

---

## Appendix B: Service Types

1. **Preventive Maintenance**
   - Scheduled inspections
   - Cleaning and calibration
   - Parts replacement (proactive)

2. **Corrective Maintenance**
   - Breakdown repairs
   - Emergency services
   - Parts replacement (reactive)

3. **Installation & Commissioning**
   - New equipment setup
   - System configuration
   - User training

---

*Document End*
