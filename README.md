# AW Schedule Manager

Connect Claude to your Oracle Primavera P6 Professional database. Ask about your schedules in plain language, edit activities and relationships, load resources and costs, or build a schedule as an XER file.

This is an independent project. It is not made, endorsed or supported by Oracle or Anthropic. Primavera and P6 are trademarks of Oracle and/or its affiliates.

## Where it works

It runs on your Windows computer, next to P6, in **Claude Desktop**, **Claude Code** and **Cowork sessions that run on your computer**. It doesn't run in Claude on the web or on mobile.

It has been tested on P6 Professional 23 with SQLite. Other versions have not been tried, and SQL Server and Oracle databases are not supported. Nothing else is needed: no Python, no packages.

## Install

### Claude Desktop (easiest)

1. Download `aw-schedule-manager-<version>.mcpb` from the latest [release](https://github.com/Ahmed-Wassel/AW-Management/releases/latest).
2. Double-click it (or drag it onto Claude Desktop > **Settings > Extensions**) and click **Install**.
3. In the extension settings, pick your **P6 database file**. Leave **Read only** on until you want Claude to edit.

**To update:** download the new `.mcpb` and open it the same way. Your settings stay.

### Claude Code

```bash
claude plugin marketplace add Ahmed-Wassel/AW-Management
claude plugin install aw-schedule-manager@aw-schedule-manager
```

This needs [Git](https://git-scm.com/downloads). Then start Claude Code and ask: `Run choose_database`. A window opens so you can browse to your P6 database file. Then run `/reload-plugins`.

The plugin starts in read-only mode. To allow editing, run `/plugin configure aw-schedule-manager`, turn off **Read only**, and start a new session. **To update:** run `/plugin`, choose the marketplace and update it.

**Use a copy of your database first.**

## Tools

**Choose the database:** `choose_database`.

**Read:** `check_compatibility`, `list_projects`, `get_open_project`, `project_summary`, `find_activities`, `activity_details`, `activity_extras`, `compare_projects`, `wbs_progress`, `list_wbs`, `list_calendars`, `list_resources`, `list_activity_codes`, `list_udfs`, `list_relationships`, `run_sql`, `list_backups`.

**Reports:** `dcma_check` (DCMA 14-point), `critical_path`, `cash_flow` (cost or units per month or week, for S-curves), `baseline_variance`, `resource_summary`.

**Edit the database:**
- Activities: `import_schedule`, `add_activity`, `update_activity`, `batch_update_activities` (a whole progress update in one step), `delete_activity`, `set_activity_fields` (calendar, types, priority, constraints, durations on many activities at once), `set_percent_complete_type`, `set_duration_type`, `set_activity_type`.
- WBS and logic: `add_wbs`, `update_wbs`, `delete_wbs`, `add_relationship`, `update_relationship`, `delete_relationship`.
- Codes, fields and notes: `create_activity_code`, `assign_activity_code`, `create_udf`, `set_udf_value`, `add_activity_notebook`, `add_activity_steps`.
- Resources and costs: `add_resources_and_costs`, `update_assignment`, `remove_resource_assignments`, `update_resource`, `delete_resource`, `add_expense`, `delete_expenses`.
- Calendars: `create_calendar` (work week, hours with breaks, holidays and yearly holidays).
- Project: `set_project_start`, `set_data_date`, `set_project_settings`, `create_baseline` (a copy of the project as its baseline), `assign_project_baseline`, `restore_backup`.

Scheduling (F9) and resource leveling stay in P6. `create_baseline` refuses, writing nothing, when a project holds data it cannot copy (funding, risks, documents and similar); make that baseline in P6.

**Write a file:** `export_schedule_xer`.

After an edit, press **F5** (Refresh Data) and then **F9** in P6. P6 calculates the dates and the critical path, not this plugin.

## Example prompts

- Summarize the project open in P6 and list its critical activities.
- Compare the baseline with the latest update and show which activities slipped more than 5 days.
- Add a 10-day activity after activity A1020, and link it to A1030.

## Safety

- **Claude can change your database.** Direct edits bypass P6's own validation and are not a method supported by Oracle.
- `import_schedule` with `replace_existing` deletes all activities, relationships and WBS of a project.
- A backup is taken before every edit, in `p6_backups\<database name>` next to the database. The last 15 are kept for each database. Restoring one needs P6 closed.
- Check that sharing project data with an AI service is allowed by your company and contract.

## Privacy

The plugin stores nothing outside your computer and sends data to no service of its own. It reads your P6 database and writes backups next to it. What a tool returns goes to Claude as part of your conversation, under your agreement with Anthropic. See the full [Privacy policy](PRIVACY.md).

## Troubleshooting

- **Windows says it protected your PC, or your antivirus blocks the program:** the program isn't signed with a paid certificate. Download it only from this page's releases; then choose **More info > Run anyway**, or allow it in your antivirus.
- **Tools report a database problem:** ask Claude to run `choose_database` and select the file again (in Claude Desktop you can also pick it in the extension settings), then run `check_compatibility`.
- **The file window doesn't appear:** check behind your other windows. If it still doesn't open, give Claude the full path of the file.
- **Changes don't appear in P6:** press F5, then F9.
- **Something else:** open a [problem report](https://github.com/Ahmed-Wassel/AW-Management/issues/new/choose). Don't attach your database: the page is public.

## Changes

See [CHANGELOG.md](CHANGELOG.md).

## Licence

Copyright (c) 2026 Ahmed Wassel. All rights reserved. AW Schedule Manager is proprietary software, free to use under the [licence agreement](LICENSE): install and use it unmodified for your own work, including commercial work. Copying, changing, reverse engineering, redistributing or renaming it is not allowed. Third-party components are listed in [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).
