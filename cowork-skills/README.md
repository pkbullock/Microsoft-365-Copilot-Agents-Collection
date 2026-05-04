# Installation

Copy to OneDrive - ```/Documents/Cowork/skills``` folder.
Refer to blog post https://pkbullock.com/blog/2026/exploring-new-cowork-agent 

## All the available tools

Here are all the tools I have available, grouped by area:

### Microsoft 365 — Email (Outlook)
ListMessages, GetMessage, SearchM365 — read/search
SendEmailWithAttachments, ReplyToMessage, ReplyAllToMessage, ReplyWithFullThread, ReplyAllWithFullThread, ForwardMessage, ForwardMessageWithFullThread
CreateDraftMessage, UpdateDraft, SendDraftMessage, AddDraftAttachments
UploadAttachment, UploadLargeAttachment, DeleteAttachment
MoveMessage, DeleteMessage, UpdateMessage, FlagEmail
ListMailFolders, GetMailFolder, CreateMailFolder
ListMailRules, CreateMailRule, UpdateMailRule, DeleteMailRule
GetAutoReplySettings, SetAutoReply, DisableAutoReply

### Microsoft 365 — Calendar
ListEvents, ListCalendarView, FindMeetingTimes
CreateEvent, UpdateEvent, DeleteEventById, CancelEvent
AcceptEvent, DeclineEvent, TentativelyAcceptEvent, ForwardEvent
GetRooms, GetUserDateAndTimeZoneSettings

### Microsoft 365 — Teams

ListTeams, GetTeam, ListChannels, GetChannel
CreateChannel, CreatePrivateChannel, UpdateChannel
ListChannelMembers, AddChannelMember, UpdateChannelMember
ListChannelMessages, PostChannelMessage, ReplyToChannelMessage
ListChats, GetChat, CreateChat, UpdateChat
ListChatMembers, AddChatMember
ListChatMessages, GetChatMessage, PostMessage, UpdateChatMessage, DeleteChatMessage
GetMyRecentTranscripts, ListMeetingTranscripts, GetMeetingTranscript

### Microsoft 365 — Files (SharePoint / OneDrive)
GetSite, SearchSites, ListSubsites
GetDefaultDrive, ListDrives, SearchDrive
GetDriveChildren, GetDriveItem, ReadFileContent, CreateFolder
ListLists, ListListColumns, ListListItems

### Microsoft 365 — People
GetMyDetails, GetUserDetails, GetMultipleUsersDetails
SearchPeople, GetManagerDetails, GetDirectReportsDetails

### Microsoft 365 — General
SearchM365 (unified search across files, email, Teams, calendar, Power BI)
QueryGraph, CallGraph (raw Graph API access)

### Workspace & Files
Read, Write, Edit, NotebookEdit
Glob, Grep, Bash

### Web & Visuals
web_search, web_fetch, search_images
 render_ui (Adaptive Cards)

### Tasks & Planning
TaskCreate, TaskUpdate, TaskGet, TaskList, TaskOutput, TaskStop
AskUserQuestion, EnterPlanMode, ExitPlanMode
EnterWorktree, ExitWorktree
Skill (invoke skills), Agent (delegate to subagents)

### Scheduled Tasks
SetupScheduledPrompt, GetScheduledPrompts, EditScheduledPrompt, DeleteScheduledPrompt

*Supplied by Skills Management*

## Documentation

Heads-up — this is a long reference. Here's the full documentation for every tool I have, organized by category:

---

## 📧 Outlook — Email

**ListMessages** — List emails ordered by date with optional filters (sender, date range, unread, flagged, has attachments, importance). Use this for "latest emails" or "unread emails." Supports pagination via `next_link`.

**GetMessage** — Get full content (subject, body, sender, attachments) of a specific email by ID. ID must come from a prior list/search call.

**SearchM365** — Unified search across files, email, Teams, calendar, Power BI. Files use semantic search; email/Teams/calendar use keyword KQL. Filterable by date and sender.

**SendEmailWithAttachments** — Compose and send an email immediately. Supports recipients (names or addresses), CC/BCC, attachments (workspace files or OneDrive URIs), and importance level.

**CreateDraftMessage** — Create a draft in your Drafts folder without sending. Pair with UpdateDraft / AddDraftAttachments / SendDraftMessage.

**UpdateDraft** — Modify an existing draft's recipients, subject, or body. Does not send.

**SendDraftMessage** — Send an existing draft by ID.

**AddDraftAttachments** — Attach workspace files to an existing draft.

**ReplyToMessage** — Reply to the sender of an email. Optional CC/BCC. Sends immediately.

**ReplyAllToMessage** — Reply to all original recipients. Optional additional CC/BCC.

**ReplyWithFullThread** — Same as ReplyToMessage but preserves the full quoted thread; supports adding new `to` recipients.

**ReplyAllWithFullThread** — Same as ReplyAllToMessage but preserves the full quoted thread.

**ForwardMessage** — Forward an email to new recipients with the quoted thread, optional comment.

**ForwardMessageWithFullThread** — Identical to ForwardMessage (alias).

**MoveMessage** — Move an email to a different folder (use folder ID or well-known name like inbox/archive/junkemail).

**DeleteMessage** — Soft-delete (moves to Deleted Items).

**UpdateMessage** — Edit mutable properties: read status, importance, categories, focused/other classification.

**FlagEmail** — Set or clear follow-up flag (flagged / notFlagged / complete).

**UploadAttachment** — Upload a small attachment (≤3 MB, base64) to a message.

**UploadLargeAttachment** — Upload a large attachment (3–150 MB, base64, chunked).

**DeleteAttachment** — Remove an attachment from a draft.

**ListMailFolders** — List inbox folders with unread counts and IDs.

**GetMailFolder** — Get details of a specific folder, optionally with child folders.

**CreateMailFolder** — Create a new mail folder.

**ListMailRules** — List inbox rules with conditions and actions.

**CreateMailRule** — Create an inbox rule. Simplified params for common conditions (sender, subject contains) and actions (move, forward, mark read, etc.).

**UpdateMailRule** — Modify an existing rule (e.g., enable/disable).

**DeleteMailRule** — Remove an inbox rule.

**GetAutoReplySettings** — Read current out-of-office state.

**SetAutoReply** — Enable OOO with internal/external messages, audience, optional schedule.

**DisableAutoReply** — Turn off OOO.

---

## 📅 Outlook — Calendar

**ListEvents** — List calendar events. Returns master series for recurring meetings (not expanded instances).

**ListCalendarView** — List events in a date range with recurring meetings expanded into instances. Use for "what's on my calendar this week."

**FindMeetingTimes** — Suggest meeting times based on attendee availability, with duration and search window.

**CreateEvent** — Create a calendar event. Defaults to 30-minute Teams meeting unless `is_online_meeting=false`. Supports recurrence patterns.

**UpdateEvent** — Modify an event (time, attendees, body, location). Use `scope=all_in_series` for recurring series.

**DeleteEventById** — Delete an event. Series scope supported.

**CancelEvent** — Cancel an event you organized, with optional message.

**AcceptEvent** — Accept a meeting invite with optional comment.

**DeclineEvent** — Decline a meeting invite.

**TentativelyAcceptEvent** — Tentatively accept.

**ForwardEvent** — Forward an event as FYI (does not add as attendee — use UpdateEvent for that).

**GetRooms** — List meeting rooms in your tenant.

**GetUserDateAndTimeZoneSettings** — Get your mailbox time zone and working hours.

---

## 💬 Teams

**ListTeams** — List teams you've joined.

**GetTeam** — Get details of a specific team.

**ListChannels** — List channels in a team.

**GetChannel** — Get details of a specific channel.

**CreateChannel** — Create a standard channel.

**CreatePrivateChannel** — Create a private channel with an owner.

**UpdateChannel** — Edit a channel's display name or description.

**ListChannelMembers** — List members of a channel.

**AddChannelMember** — Add a user to a channel (use `roles=['owner']` only for private channels).

**UpdateChannelMember** — Change a member's role (owner / member).

**ListChannelMessages** — Read recent messages from a channel.

**PostChannelMessage** — Post a message to a channel (by team_id+channel_id or names). Supports subject line, attachments, and Adaptive Cards.

**ReplyToChannelMessage** — Reply to a specific message in a channel.

**ListChats** — List your recent chats. Filter by type (oneOnOne / group / meeting), unread, or member.

**GetChat** — Get details of a specific chat.

**CreateChat** — Create a new 1:1 or group chat. Provide other participants (you're added automatically).

**UpdateChat** — Change a chat's topic.

**ListChatMembers** — List members of a chat.

**AddChatMember** — Add a member to an existing chat.

**ListChatMessages** — Read messages from a chat. Pass `person` (name/email) to find their 1:1 chat automatically. Supports keyword and date filters.

**GetChatMessage** — Get a specific message from a chat.

**PostMessage** — Send a Teams message. Pass `recipients` (names or emails) — 1 person = 1:1, 2+ = group. Use `recipients=['me']` for self-chat. Supports attachments and Adaptive Cards.

**UpdateChatMessage** — Edit the content of a chat message.

**DeleteChatMessage** — Delete a chat message.

**GetMyRecentTranscripts** — Get transcripts from your recent meetings within a date range.

**ListMeetingTranscripts** — List available transcripts for a Teams meeting (by join URL).

**GetMeetingTranscript** — Get the full text of a meeting transcript (timestamped, speaker-attributed).

---

## 📁 SharePoint & OneDrive

**GetSite** — Get a SharePoint site by hostname+path or site ID.

**SearchSites** — Search for sites by name.

**ListSubsites** — List subsites of a parent site.

**GetDefaultDrive** — Get your personal OneDrive (no args), or a SharePoint site's default doc library (with `site_id`).

**ListDrives** — List document libraries in a SharePoint site.

**SearchDrive** — Search for files/folders within a drive.

**GetDriveChildren** — List contents of a folder (by drive_id+item_id, item_path, or web_url).

**GetDriveItem** — Get metadata for a file or folder.

**ReadFileContent** — Read a file's text content. Fastest with a `download_url` from a prior list/search. Binary files (docx, pdf) saved to workspace and path returned.

**CreateFolder** — Create a new folder in a drive.

**ListLists** — List SharePoint lists in a site.

**ListListColumns** — List columns in a SharePoint list.

**ListListItems** — List items in a SharePoint list with field values.

---

## 👥 People & Profile

**GetMyDetails** — Your own profile (name, email, title, department, office).

**GetUserDetails** — Look up a user by UPN or object ID. Will not work with display names — use SearchPeople first.

**GetMultipleUsersDetails** — Look up several users at once by UPN/IDs.

**SearchPeople** — Search by name or email; resolves contacts then directory.

**GetManagerDetails** — Get a user's manager (defaults to you).

**GetDirectReportsDetails** — Get a user's direct reports.

---

## 🔌 Microsoft Graph (raw)

**QueryGraph** — Make a GET request to any Graph API endpoint.

**CallGraph** — POST/PUT/PATCH to Graph (DELETE disabled). For operations not covered by specialized tools.

**SearchM365** — Already listed under Email; spans files, email, Teams, calendar, Power BI.

---

## 🗂 Workspace File Operations

**Read** — Read a file's contents. Supports text, images, PDFs (with page ranges), and Jupyter notebooks.

**Write** — Create or overwrite a file. Must read first if file exists.

**Edit** — Make exact string replacements in a file. Use `replace_all` for renames.

**NotebookEdit** — Edit a specific cell in a Jupyter notebook (replace, insert, delete).

**Glob** — Find files by pattern (e.g., `input/**/*.xlsx`).

**Grep** — Ripgrep-powered content search. Supports regex, file-type filters, multiline, context lines.

**Bash** — Run shell commands. Supports background execution and timeouts. Working directory persists.

---

## 🌐 Web & Images

**web_search** — Bing-powered search for current information. Use parallel calls for distinct subjects.

**web_fetch** — Fetch a web page and return its full text content.

**search_images** — Find public-license images by keyword. Returns 20+ Bing-hosted thumbnails per call.

**render_ui** — Render structured data as Adaptive Cards (charts, tables, KPIs, dashboards). One call per response.

---

## ✅ Tasks & Planning

**TaskCreate** — Create a tracked task (subject, description, optional activeForm spinner text).

**TaskUpdate** — Update a task's status, owner, dependencies, or details.

**TaskGet** — Get full details of a task.

**TaskList** — List all tasks with status and dependencies.

**TaskOutput** — Read output from a background task (deprecated — prefer reading the output file).

**TaskStop** — Stop a running background task.

**AskUserQuestion** — Pose 1–4 multiple-choice questions to the user (each with 2–4 options).

**EnterPlanMode** — Enter planning mode for non-trivial implementation work.

**ExitPlanMode** — Exit plan mode after the plan file is written.

**EnterWorktree** — Create an isolated git worktree (only on explicit instruction).

**ExitWorktree** — Leave a worktree session, keeping or removing it.

**Skill** — Invoke a skill by name (e.g., `pdf`, `docx`, `daily-briefing`).

**Agent** — Delegate a task to a specialized subagent (general-purpose, Explore, Plan, deep-research-agent, statusline-setup).

---

## ⏰ Scheduled Tasks

**SetupScheduledPrompt** — Create a recurring task. Frequency: Minute / Hour / Day / Week / Month / Once. One prompt per task.

**GetScheduledPrompts** — Read your existing scheduled tasks (returns version numbers).

**EditScheduledPrompt** — Modify an existing schedule (provide version for safe updates). Use `state: paused` to pause.

**DeleteScheduledPrompt** — Permanently remove a scheduled task.

---

That's everything I can do. Want me to save this as a reference file in your output folder, or move on to the manager-report skill rewrite?