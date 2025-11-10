# App4KITAs Dashboard - Complete Functionality Documentation

**Last Updated: January 2025**  
**Based on: Actual Code Analysis**

---

## 📋 Table of Contents

- [Overview](#overview)
- [Admin Dashboard Pages](#admin-dashboard-pages)
- [Educator Dashboard Pages](#educator-dashboard-pages)
- [Super Admin Dashboard Pages](#super-admin-dashboard-pages)
- [Träger Admin Dashboard Pages](#träger-admin-dashboard-pages)
- [Shared Components](#shared-components)
- [API Services](#api-services)

---

## Overview

The App4KITAs Dashboard is a React-based web application with role-based access control. The dashboard consists of **29 pages** across 4 user roles, with comprehensive functionality for managing kindergartens, children, staff, and communications.

### Role Summary

| Role | Pages | Description |
|------|-------|-------------|
| **ADMIN** | 11 pages | Institution-level management |
| **EDUCATOR** | 5 pages | Daily operations and child care |
| **SUPER_ADMIN** | 8 pages | Platform-wide administration |
| **TRAGER_ADMIN** | 5 pages | Organization-level management |

**Total: 29 pages**

---

## Admin Dashboard Pages

### 1. Dashboard (`/admin/dashboard`)

**File:** `pages/admin/Dashboard.tsx`

**Functionality:**
- **Statistics Overview:**
  - Total children count
  - Total groups count
  - Total educators count
  - Today's check-ins count
  - Pending check-ins (children not checked in)
  - Recent activity feed
  - Quick access cards to key features

- **Quick Links:**
  - Children Management
  - Groups Management
  - Staff Management
  - Statistics
  - Reports
  - Calendar & Events
  - Communications
  - Chat

- **Personal Notebook:**
  - Private notes for admin
  - Persistent storage
  - Quick access from dashboard

- **Recent Activity:**
  - Last check-ins/outs
  - Recent updates
  - Activity timeline

**API Calls:**
- `getAdminStats()` - Dashboard statistics
- Activity log retrieval

---

### 2. Children Management (`/admin/children`)

**File:** `pages/admin/Children.tsx`

**Functionality:**
- **CRUD Operations:**
  - Create new child with full profile
  - Edit child information
  - Delete child (soft delete)
  - View child details

- **Child Profile Fields:**
  - Name, birth date
  - Photo upload and management
  - Allergies and medical conditions
  - Emergency contact information
  - Group assignment
  - Parent assignments (multiple parents)
  - Consent management (photo, data processing, marketing)

- **QR Code Management:**
  - Generate QR code for individual child
  - Bulk QR code generation for multiple children
  - QR code PDF export
  - QR code printing status tracking
  - Regenerate QR codes

- **Photo Management:**
  - Upload child photos
  - Photo preview
  - Photo deletion

- **Parent Management:**
  - Assign multiple parents to child
  - Remove parent assignments
  - View parent information

- **Search & Filter:**
  - Search by name
  - Filter by group
  - Filter by consent status
  - Pagination support

**API Calls:**
- `fetchChildren()` - List all children
- `addChild()` - Create child
- `editChild()` - Update child
- `deleteChild()` - Delete child
- `fetchChildQRCode()` - Get QR code
- `uploadChildPhoto()` - Upload photo
- `fetchGroups()` - Get groups for assignment
- `fetchParents()` - Get parents for assignment

---

### 3. Groups Management (`/admin/groups`)

**File:** `pages/admin/Groups.tsx`

**Functionality:**
- **CRUD Operations:**
  - Create new group
  - Edit group information
  - Delete group
  - View group details

- **Group Information:**
  - Group name
  - Group description
  - Institution association

- **Educator Assignment:**
  - Assign multiple educators to group
  - Remove educator from group
  - View assigned educators
  - Educator count per group

- **Child Assignment:**
  - View children in group
  - Child count per group
  - (Child assignment managed in Children page)

- **Group Statistics:**
  - Number of children
  - Number of educators
  - Group activity status

- **Search & Filter:**
  - Search by name
  - Pagination support

**API Calls:**
- `fetchGroups()` - List all groups
- `addGroup()` - Create group
- `editGroup()` - Update group
- `deleteGroup()` - Delete group
- `fetchEducators()` - Get educators for assignment
- `assignEducators()` - Assign educators to group
- `updateGroupEducators()` - Update educator assignments

---

### 4. Staff Management (`/admin/personal`)

**File:** `pages/admin/Personal.tsx`

**Functionality:**
- **CRUD Operations:**
  - Create new educator/staff member
  - Edit staff information
  - Delete staff member
  - View staff details

- **Staff Profile Fields:**
  - Name, email, phone
  - Role (EDUCATOR, ADMIN)
  - Status (active, inactive, suspended)
  - Group assignments
  - Last login timestamp
  - Avatar upload

- **Status Management:**
  - Activate/deactivate staff
  - Suspend staff accounts
  - Status badges with visual indicators

- **Password Management:**
  - Change educator password (admin function)
  - Password reset capability

- **Group Assignment:**
  - Assign staff to groups
  - View group memberships
  - Multiple group assignments

- **Activity Tracking:**
  - Last login time
  - Account status history
  - Activity indicators

- **Search & Filter:**
  - Search by name or email
  - Filter by role
  - Filter by status
  - Pagination support

**API Calls:**
- `fetchEducators()` - List all educators
- `addEducator()` - Create educator
- `editEducator()` - Update educator
- `deleteEducator()` - Delete educator
- `changeEducatorPassword()` - Change password
- `updateUserStatus()` - Update status
- `fetchGroups()` - Get groups for assignment

---

### 5. Statistics (`/admin/statistiken`)

**File:** `pages/admin/Statistiken.tsx`

**Functionality:**
- **Overview Statistics:**
  - Total children
  - Total groups
  - Total educators
  - Today's check-ins
  - Children >8h attendance
  - Recent activity count

- **Charts & Visualizations:**
  - 7-day attendance trend (Line chart)
  - Group-wise attendance (Bar chart)
  - Check-in/out patterns (Area chart)
  - Time-based analytics

- **Group Statistics:**
  - Per-group attendance rates
  - Group performance metrics
  - Group comparison charts

- **Check-in Statistics:**
  - Daily check-in counts
  - Check-in methods (QR vs Manual)
  - Check-in time distribution
  - Late arrivals tracking

- **Real-time Updates:**
  - Live statistics refresh
  - Date range filtering
  - Export capabilities

**API Calls:**
- `getAdminStats()` - Overall statistics
- `fetchCheckinStats()` - Check-in statistics
- `fetchGroups()` - Group data for charts

---

### 6. Reports (`/admin/reports`)

**File:** `pages/admin/Reports.tsx`

**Report Types (8 Total):**

#### 6.1 Daily Report (`DailyReport.tsx`)
- Today's attendance summary
- Check-ins/outs for the day
- Late arrivals
- Late pickups
- Absences
- CSV/PDF export

#### 6.2 Monthly Report (`MonthlyReport.tsx`)
- Monthly attendance trends
- Monthly statistics
- Comparison with previous month
- Group performance
- CSV/PDF export

#### 6.3 Custom Range Report (`CustomRangeReport.tsx`)
- Custom date range selection
- Attendance for selected period
- Detailed analytics
- Export functionality

#### 6.4 Late Arrivals Report (`LateArrivalsReport.tsx`)
- Children arriving late
- Late arrival patterns
- Time analysis
- Frequency tracking

#### 6.5 Late Pickups Report (`LatePickupsReport.tsx`)
- Children picked up late
- Late pickup patterns
- Time analysis
- Parent notification tracking

#### 6.6 Absence Patterns Report (`AbsencePatternsReport.tsx`)
- Absence trends
- Pattern recognition
- Frequency analysis
- Group comparisons

#### 6.7 Group Performance Report (`GroupPerformanceReport.tsx`)
- Per-group statistics
- Group comparisons
- Performance metrics
- Attendance rates

#### 6.8 Time Analytics Report (`TimeAnalyticsReport.tsx`)
- Time-based analytics
- Check-in time distribution
- Duration analysis
- Peak time identification

**Common Features:**
- Tab-based report selector
- Date range filtering
- CSV export
- PDF export
- Print functionality
- Report descriptions and help text

**API Calls:**
- Various report-specific API endpoints from `reportApi.ts`

---

### 7. Calendar & Events (`/admin/events`)

**File:** `pages/admin/Events.tsx`

**Functionality:**
- **Event Management:**
  - Create events with full details
  - Edit events
  - Delete events
  - View event details

- **Event Information:**
  - Title, description
  - Date and time
  - Location
  - Group assignments
  - RSVP tracking

- **View Modes:**
  - **Calendar View:**
    - Monthly calendar display
    - Event markers on dates
    - Click to view event details
    - Navigation (previous/next month)
  
  - **Table View:**
    - List of all events
    - Sortable columns
    - Filter by date range
    - Search functionality

- **RSVP Management:**
  - Track RSVPs per event
  - RSVP statistics
  - RSVP form for participants
  - RSVP status indicators

- **Educator Sessions (Working Hours):**
  - Create educator work sessions
  - Track working hours
  - Session management
  - Export sessions to CSV/Excel

- **Export Functions:**
  - Export events to iCal format
  - Export events to CSV
  - Export calendar view
  - Export sessions

- **Event Features:**
  - Group-based events
  - Recurring events support
  - Event reminders
  - Event notifications

**API Calls:**
- `fetchEvents()` - List events
- `createEvent()` - Create event
- `updateEvent()` - Update event
- `deleteEvent()` - Delete event
- `rsvpToEvent()` - RSVP to event
- `fetchEventRsvpStats()` - Get RSVP statistics
- `exportEvent()` - Export event data
- `exportEventCalendar()` - Export as calendar
- `fetchSessions()` - Get educator sessions
- `createSession()` - Create session
- `updateSession()` - Update session
- `deleteSession()` - Delete session
- `exportSessions()` - Export sessions

---

### 8. Communications (`/admin/communications`)

**File:** `pages/admin/Communications.tsx`

**Tab-based Interface with 4 Tabs:**

#### 8.1 Surveys Tab (`SurveysTab.tsx`)
- **Survey Management:**
  - Create surveys with questions
  - Edit surveys
  - Delete surveys
  - View survey results

- **Survey Features:**
  - Multiple question types
  - Response collection
  - Results visualization
  - Survey statistics

- **Recipients:**
  - Select groups
  - Select individual children/parents
  - Select educators

#### 8.2 Announcements Tab (`AnnouncementsTab.tsx`)
- **Announcement Management:**
  - Create announcements
  - Edit announcements
  - Delete announcements
  - Publish announcements

- **Announcement Features:**
  - Rich text content
  - Recipient selection (groups, children, parents)
  - Publishing control
  - Read tracking
  - Statistics (read/unread)

- **Recipients:**
  - Groups
  - Individual children
  - Parents
  - Educators

#### 8.3 Absence & Health Tab (`AbsenceHealthTab.tsx`)
- **Absence Reports:**
  - View parent absence reports
  - Review absence reports
  - Resolve absence reports
  - Export absence data

- **Educator Absences:**
  - Create educator absence records
  - Edit absences
  - Resolve absences
  - Export absences

- **Health Alerts:**
  - Create health bulletins
  - Activate/archive alerts
  - Acknowledgment tracking
  - Export health alerts

**API Calls:**
- `getAllSurveys()` - List surveys
- `createSurvey()` - Create survey
- `updateSurvey()` - Update survey
- `deleteSurvey()` - Delete survey
- `fetchAnnouncements()` - List announcements
- `createAnnouncement()` - Create announcement
- `deleteAnnouncement()` - Delete announcement
- `absenceHealthApi` - Absence and health APIs

---

### 9. Chat (`/admin/chat`)

**File:** `pages/admin/Chat.tsx`

**Functionality:**
- Uses shared `SharedChat` component with role="admin"
- Full chat functionality (see Shared Components section)

---

### 10. Settings (`/admin/settings`)

**File:** `pages/admin/Settings.tsx`

**Functionality:**
- **Institution Settings:**
  - Institution name
  - Address
  - Contact information
  - Opening hours (opening time, closing time)
  - Repeated closed days configuration

- **Closed Days Management:**
  - Add closed days
  - Remove closed days
  - View all closed days
  - Calendar-based selection

- **Settings Tabs:**
  - **General Settings:**
    - Basic institution information
    - Address details
  
  - **Opening Hours:**
    - Opening time
    - Closing time
    - Time format configuration
  
  - **Holidays & Closed Days:**
    - Add holidays
    - Add custom closed days
    - Remove closed days
    - Calendar view

- **Save & Validation:**
  - Form validation
  - Save settings
  - Success/error notifications
  - Settings persistence

**API Calls:**
- `getInstitutionSettings()` - Get settings
- `updateInstitutionSettings()` - Update settings
- `addClosedDay()` - Add closed day
- `removeClosedDay()` - Remove closed day

---

### 11. Reports Index (`/admin/reports`)

**File:** `pages/admin/Reports.tsx`

**Functionality:**
- Report type selector with tabs
- Navigation to individual report pages
- Report descriptions
- Quick access to all 8 report types

---

## Educator Dashboard Pages

### 1. Dashboard (`/educator/dashboard`)

**File:** `pages/educator/Dashboard.tsx`

**Functionality:**
- **Today's Overview:**
  - Today's children count
  - Checked-in children
  - Pending check-ins (not checked in yet)
  - Recent activity feed

- **Statistics Cards:**
  - Total assigned children
  - Today's check-ins
  - Pending check-ins
  - Recent activity count

- **Quick Links:**
  - Check-in/out
  - Children view
  - Notes
  - Chat
  - Personal tasks

- **Personal Notebook:**
  - Private notes for educator
  - Quick access

- **Recent Activity:**
  - Last check-ins/outs
  - Recent updates
  - Activity timeline

**API Calls:**
- `fetchTodaysChildren()` - Today's children
- `fetchPendingCheckins()` - Pending check-ins
- `fetchMyGroup()` - Educator's group
- `fetchEducatorCheckinStats()` - Check-in statistics
- `fetchRecentActivity()` - Recent activity

---

### 2. Check-in (`/educator/checkin`)

**File:** `pages/educator/Checkin.tsx`

**Functionality:**
- **Check-in/out Operations:**
  - Check-in child (CHECK_IN)
  - Check-out child (CHECK_OUT)
  - Manual time correction
  - Check-in history per child

- **Today's Children List:**
  - List of assigned children
  - Check-in status indicators
  - Quick check-in/out buttons
  - Time display

- **Statistics:**
  - Today's check-ins count
  - Checked-out count
  - Pending check-ins
  - Total children

- **Check-in Features:**
  - Time correction capability
  - Check-in notes/comments
  - Notification sending on check-in
  - Check-in history view

- **Child Information:**
  - Child name and photo
  - Group assignment
  - Check-in status
  - Last check-in time

**API Calls:**
- `fetchTodaysChildren()` - Today's children
- `checkinKind()` - Perform check-in/out
- `fetchChildHistory()` - Check-in history
- `correctCheckinTime()` - Correct check-in time
- `sendNotification()` - Send notifications

---

### 3. Children View (`/educator/kinder`)

**File:** `pages/educator/Kinder.tsx`

**Functionality:**
- **Assigned Children List:**
  - View all assigned children
  - Child details
  - Group information
  - Check-in status

- **Child Information:**
  - Name, photo
  - Group assignment
  - Parents information
  - Medical information (allergies, conditions)
  - Consent status

- **Filtering:**
  - Filter by group
  - Search by name
  - Date-based filtering

- **Quick Actions:**
  - View child details
  - Check-in/out
  - View notes
  - Open chat

**API Calls:**
- `fetchMyGroup()` - Get educator's group
- `fetchTodaysChildren()` - Get children

---

### 4. Notes (`/educator/notizen`)

**File:** `pages/educator/Notizen.tsx`

**Functionality:**
- **Note Management:**
  - Create notes for children
  - Edit notes
  - Delete notes
  - Bulk delete notes
  - View note details

- **Note Types:**
  - GENERAL - General observations
  - BEHAVIOR - Behavioral notes
  - HEALTH - Health-related notes
  - DEVELOPMENT - Development notes
  - INCIDENT - Incident reports

- **Note Features:**
  - Rich text content
  - File attachments (photos, PDFs)
  - Private notes (educator-only)
  - Note search
  - Filter by type, child, date
  - Sort options

- **Note Display:**
  - Card-based layout
  - Note type indicators
  - Attachment previews
  - Timestamp display
  - Child information

- **Export:**
  - Export notes to CSV
  - Export with attachments
  - Filtered export

**API Calls:**
- `getNotes()` - List all notes
- `getChildNotes()` - Get notes for specific child
- `createNote()` - Create note
- `updateNote()` - Update note
- `deleteNote()` - Delete note
- `deleteMultipleNotes()` - Bulk delete
- `exportNotes()` - Export notes
- `searchNotes()` - Search notes

---

### 5. Chat (`/educator/chat`)

**File:** `pages/educator/Chat.tsx`

**Functionality:**
- Uses shared `SharedChat` component with role="educator"
- Full chat functionality (see Shared Components section)

---

## Super Admin Dashboard Pages

### 1. Dashboard (`/super-admin/dashboard`)

**File:** `pages/super_admin/Dashboard.tsx`

**Functionality:**
- **Platform Statistics:**
  - Total Träger (organizations)
  - Total institutions
  - Total users (all roles)
  - Active users
  - Inactive users

- **Quick Links:**
  - Träger management
  - Institutions management
  - Statistics
  - Reports
  - Educators management
  - Parents management
  - GDPR compliance

- **Activity Log:**
  - Recent platform activity
  - System-wide events
  - Activity timeline

- **Personal Notebook:**
  - Private notes for super admin

**API Calls:**
- `getSuperAdminStats()` - Platform statistics
- Activity log retrieval

---

### 2. Träger Management (`/super-admin/traeger`)

**File:** `pages/super_admin/Traeger.tsx`

**Functionality:**
- **Träger CRUD:**
  - Create Träger (organization)
  - Edit Träger information
  - Delete Träger
  - View Träger details

- **Träger Information:**
  - Name
  - Address
  - Contact email
  - Contact phone
  - Created by (Super Admin)
  - Creation date

- **Träger-Admin Management:**
  - Create Träger-Admin users
  - Edit Träger-Admin information
  - Delete Träger-Admin
  - Assign Träger-Admin to Träger
  - View all Träger-Admins

- **Träger-Admin Information:**
  - Name, email
  - Password management
  - Träger assignment
  - Status (active/inactive)
  - Last login

- **Search & Filter:**
  - Search Träger by name
  - Search Träger-Admins
  - Pagination support

**API Calls:**
- `getAllTraeger()` - List all Träger
- `createTraeger()` - Create Träger
- `updateTraeger()` - Update Träger
- `deleteTraeger()` - Delete Träger
- `getAllTraegerAdmins()` - List Träger-Admins
- `createTraegerAdmin()` - Create Träger-Admin
- `updateTraegerAdmin()` - Update Träger-Admin
- `deleteTraegerAdmin()` - Delete Träger-Admin
- `fetchAllUsers()` - Get all users
- `updateUserStatus()` - Update user status

---

### 3. Institutions (`/super-admin/institutionen`)

**File:** `pages/super_admin/Institutionen.tsx`

**Functionality:**
- **Institution CRUD:**
  - Create institution
  - Edit institution
  - Delete institution
  - View institution details

- **Institution Information:**
  - Name, address
  - Träger assignment (required)
  - Opening hours
  - Contact information
  - Settings

- **Institution Statistics:**
  - Children count
  - Groups count
  - Educators count
  - Activity metrics

- **Search & Filter:**
  - Search by name
  - Filter by Träger
  - Pagination support

**API Calls:**
- Institution management APIs
- Statistics APIs

---

### 4. Statistics (`/super-admin/statistiken`)

**File:** `pages/super_admin/Statistiken.tsx`

**Functionality:**
- **Platform-wide Statistics:**
  - User growth over time
  - Active users
  - Check-in trends
  - Message volume
  - Notification statistics
  - Failed logins
  - Group attendance
  - Check-in methods

- **Charts & Visualizations:**
  - User growth charts
  - Activity trends
  - Platform-wide metrics
  - Comparative analytics

- **Date Range Filtering:**
  - Custom date ranges
  - Time period selection
  - Export capabilities

**API Calls:**
- `getSuperAdminStats()` - Platform statistics
- Various analytics APIs

---

### 5. Reports (`/super-admin/reports`)

**File:** `pages/super_admin/Reports.tsx`

**Functionality:**
- **Platform Reports:**
  - User growth report
  - Active users report
  - Check-in trends report
  - Active groups report
  - Message volume report
  - Notification stats report
  - Failed logins report
  - Group attendance report
  - Check-in methods report
  - Platform statistics report

- **Export Functions:**
  - CSV export
  - PDF export
  - Bulk export

**API Calls:**
- Platform report APIs from `reportApi.ts`

---

### 6. Educators (`/super-admin/educators`)

**File:** `pages/super_admin/Educators.tsx`

**Functionality:**
- **Platform-wide Educator Management:**
  - View all educators across all institutions
  - Educator details
  - Institution assignment
  - Status tracking

- **Educator Information:**
  - Name, email, phone
  - Institution
  - Groups
  - Status (active/inactive)
  - Last login

- **Search & Filter:**
  - Search by name/email
  - Filter by institution
  - Filter by status
  - Pagination support

**API Calls:**
- Platform-wide user APIs

---

### 7. Parents (`/super-admin/parents`)

**File:** `pages/super_admin/Parents.tsx`

**Functionality:**
- **Platform-wide Parent Management:**
  - View all parents across all institutions
  - Parent details
  - Children assignments
  - Status tracking

- **Parent Information:**
  - Name, email, phone
  - Institution
  - Children
  - Status (active/inactive)
  - Last login

- **Search & Filter:**
  - Search by name/email
  - Filter by institution
  - Filter by status
  - Pagination support

**API Calls:**
- Platform-wide user APIs

---

### 8. GDPR Compliance (`/super-admin/gdpr`)

**File:** `pages/super_admin/GDPRCompliancePage.tsx`

**Functionality:**
- **GDPR Dashboard:**
  - Audit logs
  - Pending deletions
  - Data retention management
  - Compliance reports

- **Data Management:**
  - Data export requests
  - Deletion requests
  - Anonymization
  - Deep cleanup

- **Compliance Tools:**
  - Consent tracking
  - Data retention periods
  - Audit trail
  - Compliance reports

**API Calls:**
- GDPR management APIs from `gdprApi.ts`

---

## Träger Admin Dashboard Pages

### 1. Dashboard (`/traeger-admin/dashboard`)

**File:** `pages/traeger_admin/Dashboard.tsx`

**Functionality:**
- **Träger Statistics:**
  - Total children (Träger-wide)
  - Children >8h attendance
  - Total educators
  - Total institutions
  - Inactive users (last 4 weeks)
  - Failed logins (last 30 days)

- **Quick Links:**
  - Institutions management
  - Statistics
  - User management
  - Settings

- **Alerts:**
  - Inactive users warning
  - Failed login alerts
  - Security notifications

**API Calls:**
- `getTraegerStats()` - Träger statistics
- `getInactiveUsers()` - Inactive users
- `getFailedLogins()` - Failed logins

---

### 2. Institutions (`/traeger-admin/einrichtungen`)

**File:** `pages/traeger_admin/Einrichtungen.tsx`

**Functionality:**
- **Institution Management (Träger-wide):**
  - View all institutions in Träger
  - Create new institution
  - Edit institution
  - Delete institution
  - View institution details

- **Institution Information:**
  - Name, address
  - Contact information
  - Settings
  - Statistics per institution

- **Institution Statistics:**
  - Children count per institution
  - Educators count per institution
  - Activity metrics

- **Search & Filter:**
  - Search by name
  - Pagination support

**API Calls:**
- Träger Admin institution APIs

---

### 3. Statistics (`/traeger-admin/statistiken`)

**File:** `pages/traeger_admin/Statistiken.tsx`

**Functionality:**
- **Träger-wide Statistics:**
  - Total children (all institutions)
  - Children >8h (all institutions)
  - Total educators
  - Per-institution breakdown
  - Inactive users
  - Failed logins

- **Charts & Visualizations:**
  - Träger-wide trends
  - Per-institution comparison
  - Activity charts

- **Date Range Filtering:**
  - Custom date ranges
  - Export capabilities

**API Calls:**
- Träger Admin statistics APIs

---

### 4. Users (`/traeger-admin/benutzer`)

**File:** `pages/traeger_admin/Benutzer.tsx`

**Functionality:**
- **User Management (Träger-wide):**
  - View all Admins and Educators in Träger
  - Create new users (Admin, Educator)
  - Edit user information
  - Delete users
  - Block/unblock users

- **User Information:**
  - Name, email, phone
  - Role (ADMIN, EDUCATOR)
  - Institution assignment
  - Status (active/inactive)
  - Last login

- **User Features:**
  - Password management
  - Status updates
  - Block/unblock functionality
  - Inactive user identification

- **Search & Filter:**
  - Search by name/email
  - Filter by role
  - Filter by institution
  - Filter by status
  - Pagination support

**Note:** Parents cannot be managed by Träger-Admin

**API Calls:**
- Träger Admin user management APIs

---

### 5. Settings (`/traeger-admin/einstellungen`)

**File:** `pages/traeger_admin/Einstellungen.tsx`

**Functionality:**
- **Träger Settings:**
  - Träger information
  - Contact details
  - Settings configuration
  - (Placeholder for future features)

**API Calls:**
- Träger settings APIs

---

## Shared Components

### Chat Component (`SharedChat.tsx`)

**Location:** `components/chat/SharedChat.tsx`

**Functionality:**
- **Real-time Messaging:**
  - WebSocket-based communication
  - Direct messages (1-to-1)
  - Group conversations
  - Message reactions (emojis)
  - Typing indicators
  - Read receipts
  - Online status

- **Message Features:**
  - Text messages
  - File attachments (images, PDFs)
  - Message editing
  - Message deletion
  - Message search
  - Message pagination

- **Conversation Management:**
  - Create new conversations
  - Conversation list
  - Conversation settings
  - Participant management

- **UI Features:**
  - Full-screen chat interface
  - Responsive design
  - Dark mode support
  - File upload
  - Image viewer
  - Message status indicators

**API Calls:**
- `conversationApi.ts` - All conversation APIs
- WebSocket service for real-time updates

---

## API Services

The dashboard uses **29 API service files** located in `services/`:

1. `absenceApi.ts` - Absence reports
2. `absenceHealthApi.ts` - Absence and health alerts
3. `activityApi.ts` - Activity logs
4. `adminApi.ts` - Admin-specific APIs
5. `announcementsApi.ts` - Announcements
6. `apiClient.ts` - Base API client
7. `authApi.ts` - Authentication
8. `calendarApi.ts` - Calendar and sessions
9. `conversationApi.ts` - Chat conversations
10. `dokugenApi.ts` - AI document generation
11. `educatorApi.ts` - Educator-specific APIs
12. `eventApi.ts` - Events
13. `gdprApi.ts` - GDPR compliance
14. `healthAlertsApi.ts` - Health alerts
15. `institutionSettingsApi.ts` - Institution settings
16. `messagingApi.ts` - Messaging
17. `noteApi.ts` - Notes
18. `notificationsApi.ts` - Notifications
19. `notificationService.ts` - Notification service
20. `offlineService.ts` - Offline support
21. `personalTaskApi.ts` - Personal tasks
22. `profileApi.ts` - User profile
23. `recipientsService.ts` - Recipient management
24. `reportApi.ts` - Reports
25. `superAdminApi.ts` - Super Admin APIs
26. `surveysApi.ts` - Surveys
27. `traegerAdminApi.ts` - Träger Admin APIs
28. `uploadApi.ts` - File uploads
29. `websocketService.ts` - WebSocket service

---

## Summary

### Page Count by Role

| Role | Pages | Details |
|------|-------|---------|
| **ADMIN** | 11 | Dashboard, Children, Groups, Personal, Statistiken, Reports (8 types), Events, Communications, Chat, Settings |
| **EDUCATOR** | 5 | Dashboard, Checkin, Kinder, Notizen, Chat |
| **SUPER_ADMIN** | 8 | Dashboard, Traeger, Institutionen, Statistiken, Reports, Educators, Parents, GDPR |
| **TRAGER_ADMIN** | 5 | Dashboard, Einrichtungen, Statistiken, Benutzer, Einstellungen |
| **Total** | **29** | |

### Key Features Across All Roles

- ✅ Role-based access control
- ✅ Real-time updates (WebSocket)
- ✅ Responsive design
- ✅ Dark mode support
- ✅ Search and filtering
- ✅ Pagination
- ✅ Export functionality (CSV, PDF)
- ✅ File uploads
- ✅ Notifications
- ✅ Activity logging
- ✅ GDPR compliance tools

---

**Last Updated:** January 2025  
**Documentation Status:** ✅ Complete and Accurate

