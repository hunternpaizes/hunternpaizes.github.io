# User Guide (Draft)

## Audience
This guide supports all Super Data Viewer personas: Administrators, Advanced Users, Regular Users, Read-only Users, and Visitors. It outlines the core workflows and UI patterns that will be available in the platform.

## Getting Started
1. Navigate to the Super Data Viewer web application in a supported browser.
2. Sign up with a corporate email address. Complete email verification to activate the account.
3. Upon first login, select your preferred language and theme. Accessibility settings (contrast, text size, screen reader hints) can be configured under **Settings → Accessibility**.

## Workspace Layout
- The home screen presents a multi-panel workspace. Panels can be resized, dragged, and docked.
- Saved layouts are accessible from the **Workspace Library**, allowing users to restore configurations across sessions.
- Keyboard shortcuts (e.g., `Ctrl + /`) open the command palette for fast navigation.

## Data Ingestion Workflow
1. Click **Import Data** and choose between local upload, database connector, or remote storage reference.
2. Review the preview sample, adjust column selection, and apply optional preprocessing filters.
3. Assign tags, descriptions, and default permission groups before launching the import job.
4. Track progress in the **Imports** dashboard, where you can view logs, retry failures, or roll back versions.

## Analysis Pipelines
- Create a pipeline by chaining operations from the **Processing Library**. Each step exposes parameter controls with validation hints.
- Save parameter configurations as templates for reuse.
- Schedule pipelines to run on a recurrence or trigger them manually. Notifications can be delivered via email or in-app alerts upon completion.

## Script Execution
- Upload Python scripts in the **Scripts** module. Scripts run in a sandbox with resource limits defined by administrators.
- Input datasets are referenced by ID; outputs are registered as derived datasets or downloadable artifacts.
- Review execution logs and performance metrics to optimize scripts.

## Visualization
- Assemble dashboards using drag-and-drop chart widgets. Each widget can bind to datasets, filters, and shared crosshair states.
- Use the **Inspector** panel to configure axes, color palettes, legends, and annotations.
- Export visualizations as PNG, SVG, or PDF, or share live dashboards with collaborators via link-based access (role-dependent).

## Collaboration Features
- Users with appropriate permissions can invite collaborators to workspaces, assign roles, and leave annotations on datasets.
- Audit trails record edits, comments, and approvals for compliance review.

## Account & Security Management
- Manage API tokens, multi-factor authentication, and session history under **Profile → Security**.
- Administrators can provision roles, review audit logs, and configure organization-wide policies from the **Admin Console**.

## Help & Support
- Contextual help icons provide inline documentation relevant to each module.
- The **Help Center** links to tutorials, FAQ, and release notes. Support tickets can be submitted directly from the UI.
- Accessibility resources include keyboard shortcut lists, screen reader descriptions, and support contact information for accommodations.
