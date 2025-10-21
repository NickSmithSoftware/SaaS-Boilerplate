# Studio Flow - Project Requirements Document

## Project Overview

**Studio Flow** is a creative workflow management platform designed to help creative teams (designers, video editors, content creators, etc.) manage projects, collaborate efficiently, and deliver exceptional results.

This is a **demo application** built on the Next.js SaaS Boilerplate template, rebranded and customized for the creative workflow use case.

---

## Core Purpose

Studio Flow aims to provide creative teams with:
- Centralized project management
- Team collaboration tools
- Asset organization and versioning
- Timeline and milestone tracking
- Client feedback integration
- Workflow automation capabilities

---

## Target Users

### Primary Users
- **Creative Team Members**: Designers, video editors, photographers, content creators
- **Creative Directors**: Team leaders who need to oversee multiple projects
- **Project Managers**: Coordinators managing timelines and deliverables
- **Clients**: External stakeholders who need to review and approve work

### User Personas
1. **Sarah - Freelance Designer** (Free Plan)
   - Solo creative professional
   - Needs to organize personal projects
   - Wants to share work with clients for feedback

2. **Tech Startup Creative Team** (Professional Plan)
   - 5-15 team members
   - Multiple concurrent projects
   - Needs collaboration and asset management

3. **Marketing Agency** (Enterprise Plan)
   - Large team (50+ members)
   - High volume of client projects
   - Requires advanced permissions and integrations

---

## Key Features (Demo Implementation)

### 1. **Project Management Dashboard**
- [ ] Project list view with status indicators
- [ ] Project cards showing key information (name, status, deadline, team members)
- [ ] Ability to create/edit/delete projects
- [ ] Project filtering and search
- [ ] Project templates for common workflows

### 2. **Task/Project Board**
- [ ] Kanban-style board view (To Do, In Progress, Review, Complete)
- [ ] Task cards with assignees and due dates
- [ ] Drag-and-drop functionality (visual only for demo)
- [ ] Task creation and editing
- [ ] Task comments/notes

### 3. **Team Collaboration**
- [ ] Team member directory
- [ ] Role-based access (inherited from template)
- [ ] Activity feed showing recent project updates
- [ ] @mention functionality in comments
- [ ] Notification system (mock for demo)

### 4. **Asset Management**
- [ ] File upload interface (UI only for demo)
- [ ] Asset library view with thumbnails
- [ ] Version history display
- [ ] Asset tagging and categorization
- [ ] Quick preview functionality

### 5. **Timeline & Milestones**
- [ ] Gantt-style timeline view (simplified)
- [ ] Milestone markers
- [ ] Project deadline indicators
- [ ] Progress visualization

### 6. **Client Feedback Portal**
- [ ] Simple feedback form
- [ ] Approval workflow (mock)
- [ ] Feedback history view
- [ ] Status indicators (pending, approved, changes requested)

### 7. **Settings & Configuration**
- [ ] Workspace settings
- [ ] Team management (using existing multi-tenancy)
- [ ] Notification preferences
- [ ] Integration settings (UI only)

---

## Technical Stack (Inherited from Template)

- **Framework**: Next.js 14 (App Router)
- **Language**: TypeScript
- **Styling**: Tailwind CSS + Shadcn UI components
- **Authentication**: Clerk
- **Database**: PostgreSQL with Drizzle ORM
- **Payments**: Stripe (demo mode)
- **Internationalization**: next-intl (English + French)
- **State Management**: React hooks + server components
- **Forms**: React Hook Form + Zod validation

---

## Database Schema Requirements

### Core Tables Needed

#### 1. **Projects**
```typescript
{
  id: string (uuid)
  organizationId: string (from Clerk)
  name: string
  description: string
  status: enum ('planning', 'active', 'review', 'completed', 'archived')
  startDate: date
  deadline: date
  createdBy: string (userId)
  createdAt: timestamp
  updatedAt: timestamp
}
```

#### 2. **Tasks**
```typescript
{
  id: string (uuid)
  projectId: string (FK)
  title: string
  description: string
  status: enum ('todo', 'in_progress', 'review', 'completed')
  priority: enum ('low', 'medium', 'high', 'urgent')
  assignedTo: string (userId)
  dueDate: date
  orderIndex: number
  createdAt: timestamp
  updatedAt: timestamp
}
```

#### 3. **Comments**
```typescript
{
  id: string (uuid)
  taskId: string (FK)
  userId: string
  content: text
  createdAt: timestamp
  updatedAt: timestamp
}
```

#### 4. **Assets** (Mock/UI only for demo)
```typescript
{
  id: string (uuid)
  projectId: string (FK)
  name: string
  type: string (file extension)
  url: string (placeholder)
  version: number
  uploadedBy: string (userId)
  createdAt: timestamp
}
```

#### 5. **Milestones**
```typescript
{
  id: string (uuid)
  projectId: string (FK)
  title: string
  description: string
  dueDate: date
  isCompleted: boolean
  createdAt: timestamp
}
```

---

## User Interface Requirements

### Design Principles
- **Clean & Modern**: Professional aesthetic suitable for creative professionals
- **Visual**: Heavy use of cards, colors, and icons
- **Intuitive**: Clear navigation and obvious actions
- **Responsive**: Works on desktop, tablet, and mobile

### Color Scheme
- **Primary**: Creative/vibrant color (blue/purple gradient)
- **Success**: Green for completed tasks/projects
- **Warning**: Yellow/orange for approaching deadlines
- **Danger**: Red for overdue items
- **Neutral**: Grays for backgrounds and secondary elements

### Key UI Components
- Project cards with status badges
- Kanban board with drag-drop zones
- Timeline/Gantt chart (simplified)
- File upload dropzone
- Activity feed with timestamps
- User avatars and team displays

---

## Demo Data Requirements

### Sample Projects
1. **Brand Identity Redesign**
   - Status: In Progress
   - 5 tasks across different stages
   - 3 team members assigned
   - Due in 2 weeks

2. **Product Launch Video**
   - Status: Review
   - 8 tasks (mostly completed)
   - 4 team members
   - Due in 1 week

3. **Social Media Campaign Q4**
   - Status: Planning
   - 12 tasks in planning phase
   - 2 team members
   - Due in 1 month

### Sample Tasks
- Mix of completed, in-progress, and pending tasks
- Various priorities
- Different assignees
- Some with comments/notes

### Sample Team Members
- 5-6 mock team members with roles (Designer, Video Editor, Creative Director, etc.)
- Profile pictures (avatars)
- Different activity levels

---

## Pricing Plans (Already Updated)

### Free Plan - $0/month
- 3 team members
- 1 project
- 5 GB storage
- Basic features

### Professional Plan - $29/month
- 15 team members
- 5 projects
- 100 GB storage
- Advanced collaboration
- Priority support

### Enterprise Plan - $99/month
- 1000 team members
- 100 projects
- 1000 GB storage
- Custom integrations
- Dedicated support
- Advanced security

---

## Pages Structure

```
/
├── [locale]/
│   ├── (landing)/
│   │   ├── page.tsx                    # Landing page (already branded)
│   │   ├── pricing/                    # Pricing page (already exists)
│   │   └── about/                      # About Studio Flow (optional)
│   │
│   ├── (auth)/
│   │   ├── sign-in/                    # Clerk auth (exists)
│   │   ├── sign-up/                    # Clerk auth (exists)
│   │   │
│   │   └── dashboard/
│   │       ├── page.tsx                # Dashboard home (exists, needs update)
│   │       ├── projects/               # NEW: Projects list
│   │       │   ├── page.tsx            # Projects overview
│   │       │   ├── [id]/               # Project detail
│   │       │   │   ├── page.tsx        # Project detail view
│   │       │   │   ├── board/          # Kanban board
│   │       │   │   ├── timeline/       # Timeline view
│   │       │   │   └── assets/         # Asset library
│   │       │   └── new/                # Create project
│   │       │
│   │       ├── tasks/                  # Tasks overview (repurpose todos)
│   │       ├── team/                   # Team directory
│   │       ├── activity/               # Activity feed
│   │       ├── members/                # Team management (exists)
│   │       └── settings/               # Settings (exists)
│   │
│   └── (marketing)/
│       └── docs/                       # Documentation (optional)
```

---

## Implementation Phases

### Phase 1: Foundation (Current)
- [x] Rebrand to Studio Flow
- [x] Update all copy and translations
- [x] Update pricing structure
- [x] Remove commitlint
- [x] Secure .env file
- [ ] Create this requirements doc

### Phase 2: Database & Models
- [ ] Design and create database schema
- [ ] Create Drizzle ORM models
- [ ] Run migrations
- [ ] Create seed data script

### Phase 3: Core Features
- [ ] Projects dashboard and CRUD operations
- [ ] Task management (refactor existing todos feature)
- [ ] Team directory
- [ ] Activity feed

### Phase 4: Advanced Features
- [ ] Kanban board view
- [ ] Timeline/milestone visualization
- [ ] Asset management UI
- [ ] Comments system

### Phase 5: Polish & Demo
- [ ] Add sample data
- [ ] Refine UI/UX
- [ ] Add loading states and animations
- [ ] Create demo video/screenshots
- [ ] Documentation

---

## Non-Functional Requirements

### Performance
- Page load time < 2 seconds
- Smooth animations and transitions
- Optimistic UI updates where possible

### Security
- Multi-tenancy isolation (inherited from template)
- Role-based access control
- Secure API routes
- Input validation and sanitization

### Accessibility
- WCAG 2.1 AA compliance
- Keyboard navigation
- Screen reader support
- Proper semantic HTML

### Browser Support
- Chrome/Edge (latest 2 versions)
- Firefox (latest 2 versions)
- Safari (latest 2 versions)
- Mobile browsers (iOS Safari, Chrome Mobile)

---

## Out of Scope (For Demo)

These features are intentionally excluded or mocked for the demo:
- ❌ Real file uploads and storage
- ❌ Real-time collaboration (WebSockets)
- ❌ Email notifications
- ❌ Third-party integrations (Slack, Google Drive, etc.)
- ❌ Advanced reporting and analytics
- ❌ Time tracking
- ❌ Invoice generation
- ❌ Mobile apps

---

## Success Criteria

The demo is successful if:
1. ✅ All pages load without errors
2. ✅ User can navigate through the entire workflow
3. ✅ CRUD operations work for projects and tasks
4. ✅ UI is polished and professional
5. ✅ Multi-tenancy works (team switching)
6. ✅ Pricing and billing flow is clear
7. ✅ Demo data showcases all features
8. ✅ Responsive design works on mobile

---

## Timeline Estimate

- **Phase 1**: Completed ✓
- **Phase 2**: 2-3 hours (database setup)
- **Phase 3**: 4-6 hours (core features)
- **Phase 4**: 4-6 hours (advanced features)
- **Phase 5**: 2-3 hours (polish)

**Total Estimated Time**: 12-18 hours for full implementation

---

## Next Steps

1. ✅ Review and approve this requirements document
2. Create database schema and migrations
3. Generate seed data
4. Build projects dashboard
5. Implement task/project board
6. Add remaining features iteratively
7. Polish and prepare demo

---

## Notes & Considerations

- This is a **demo application** - focus on visual appeal and user experience over complex business logic
- Leverage existing template features (auth, multi-tenancy, billing) wherever possible
- Use placeholder/mock data for features that would require external services
- Prioritize the "happy path" user journey
- Keep code clean and well-documented for showcase purposes

---

**Document Version**: 1.0  
**Last Updated**: October 20, 2025  
**Status**: Draft - Ready for Review
