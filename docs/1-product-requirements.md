# WOLA (Work Out Loud Agent) - Product Requirements Document

## Overview
WOLA (Work Out Loud Agent) is an agentic AI solution designed to automatically generate a daily summary of a user's work activities, grouped by customer, using data from Microsoft Exchange (email and calendar) and Microsoft Teams. The summary is delivered to the user via email and is also accessible through a dashboard. WOLA is intended for individual use and prioritizes privacy, security, and minimal user intervention.

---

## 1. Data Sources & Integrations
- **Email:** Microsoft Exchange (sent emails only)
- **Calendar:** Microsoft Exchange ("busy"/"meeting" events, including out-of-office/leave detection)
- **Teams:** Microsoft Teams (messages sent by the user)
- **Authentication:** Azure Entra ID OAuth2 (user authentication required)
- **APIs:** Microsoft Graph API with minimal permissions for reading emails, calendar events, and Teams messages

## 2. User Scope & Access
- **Intended User:** Individual (not multi-user/organization-wide)
- **Summary Generation:** Automatic, daily
- **Authentication Handling:** Prompt user to re-authenticate if required/expired
- **Permissions:** Request only the minimum Microsoft Graph API permissions needed

## 3. Summary Generation
- **Emails:** Only sent emails are included
- **Calendar:** Only "busy"/"meeting" events; detect and record leave/out-of-office
- **Teams:** Only messages sent by the user, regardless of channel
- **Customer Identification:** By email domain and calendar invite
- **Manual Correction:** Users can manually correct/override customer assignments
- **No Keywords/Tags:** No additional filters or tags for customer identification

## 4. Output & Delivery
- **Delivery:** Email to the user; optional dashboard view
- **Format:** Markdown
- **Historical Access:** Summaries stored in a secure database or cloud storage
- **Retention:** Configurable by organizational policy (e.g., 6 months, 1 year)

## 5. Customer Identification
- **Method:** By email domain and calendar invite
- **Manual Override:** Supported for user corrections

## 6. Privacy & Security
- **Data Retention/Compliance:** No specific requirements (e.g., GDPR)
- **Anonymization/Redaction:** Not required
- **Permissions:** Minimal, as per Microsoft Graph API best practices

## 7. Leave/No Activity Days
- **Detection:** Calendar out-of-office events and manual input
- **Prompting:** WOLA prompts the user if no activity is detected for a day

## 8. Platform & Deployment
- **Platforms:** Microsoft Teams bot and web app
- **Hosting:** Azure (cloud-first), but must also be runnable locally for development/testing

## 9. Extensibility & Customization
- **Customization:** No user customization of summary rules, grouping, or output format
- **Plugins/Integrations:** No support for plugins or future integrations

---

## 10. Non-Functional Requirements
- **Security:** All data access and storage must follow Azure security best practices
- **Performance:** Daily summaries should be generated and delivered within 1 hour of the end of the user's workday
- **Reliability:** The system should handle API failures gracefully and retry as needed
- **Usability:** Minimal user setup; clear prompts for authentication and manual corrections

## 11. Out of Scope
- Multi-user/organization-wide deployment
- Support for non-Microsoft platforms (e.g., Gmail, Google Calendar, Slack)
- Customization of summary logic or output format
- Plugin or extension support

---

## 12. Open Questions / Future Considerations
- Retention period for summaries should be confirmed with organizational policy
- Dashboard design and features to be defined in a future document

---

## Appendix: Example Summary Format

```
## Daily Work Summary for 2025-07-21

### Customer: Contoso Ltd
- Sent project update email regarding Q3 deliverables
- Attended weekly status meeting
- Sent Teams message: "Shared the new roadmap document"

### Customer: Fabrikam Inc
- Sent follow-up email on support ticket #1234

### Internal
- Attended internal team sync
- Sent Teams message: "Reviewed the new onboarding process"

```

---

This document defines the product requirements for WOLA and should be used as the basis for design and implementation.
