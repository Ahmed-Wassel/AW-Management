# Changelog

## 1.6.0
- **Update quality and reports** (12 new tools; nothing in P6 is changed by the report tools). Reports have no fixed layout: the
  data tools give the figures and `create_pdf_report` / `create_excel_report` write exactly the sections, tables, charts and
  wording the user asks for each time.
  - `audit_update`: checks an update before it is submitted (In Progress with zero remaining duration, out-of-sequence progress,
    actuals after the data date, activities due but not started; and with the previous update: reversed actuals, changed actual
    dates, added or removed activities, logic changes).
  - `compare_updates`: the figures of a comparison between two updates (summary, float lost by WBS, worst activities, reversed
    actuals, late starts, zero remaining duration, logic and duration changes, drivers), picked part by part.
  - `create_pdf_report` and `create_excel_report`: write a report with the blocks (headings, text, bullets, tables, bar charts) or
    sheets you give, in the order you give.
  - `delay_windows`: delay analysis over a series of updates with the causes that touch the critical activities.
  - `create_update`: the next update as a copy of the last one with a new data date.
  - `import_progress_from_excel`: progress from an .xlsx or .csv, checked first (dry run), then applied in one transaction.
  - `export_excel` (data dumps: activities, relationships, assignments, float comparison), `look_ahead`, `earned_value` (by WBS),
    `resource_histogram` and `what_if_duration` (a float-based estimate; F9 in P6 gives the exact answer).
  - Reports are written to Documents\AW Schedule Manager unless you give a path. The PDF is Latin text only (Arabic shows as ?);
    Excel keeps all text.
- **Projects.** `create_project` (a new empty project under an EPS node, with the settings of a template project),
  `copy_project` (a whole project as a separate one, optionally under another EPS node) and `delete_project` (the project
  with all its data; asks for its ID again as a second check, is refused while the project is open in P6 or while it has
  baselines unless you say so). `update_expense` changes an existing expense.
- Activity codes can now have a colour per value (`color` in `create_activity_code`, RRGGBB).
- **Admin and Enterprise data.** 11 new tools for the items of P6's Enterprise and Admin menus:
  - Cost accounts, funding sources, OBS and roles: `list_enterprise_items`, `edit_enterprise_item` (create, rename, move,
    delete) and `assign_cost_account` (put an account on resource assignments and/or expenses).
  - Resource, project, role and assignment codes: `list_codes`, `create_code_values`, `assign_code` (resources, projects,
    roles) and `delete_code`.
  - EPS: `manage_eps` (create, rename, move, delete nodes) and `move_project_to_eps`.
  - Resource shifts and resource curves: `manage_resource_shift`, `manage_resource_curve`.
  - Nothing that is still used (assigned codes, accounts on assignments, OBS on a project, roles on resources, EPS holding
    projects) is ever deleted; the tool says where it is used. Built-in P6 curves are protected.
- 87 tools in all.
- Not covered (do these in P6): Issues, Risks and Thresholds (the tool must first see how P6 stores them), Tracking,
  Project Portfolios, Activity Step Templates, Stored Images, External Applications, editing an existing calendar, and
  assigning assignment codes.

## 1.5.2
- The backup note is shown once: every edit still makes an automatic backup, but only the first edit of a session
  reports the backup file, so Claude no longer repeats it after every change (`list_backups` shows them all).

## 1.5.1
- `check_for_updates`: ask Claude whether a newer version is out, with the download link and what's new.
- **Check for updates** setting (off by default): when on, once a day you are told about a new version.
- Settings now say to turn the extension off and on after a change, and the install steps point to
  **Settings > Desktop app > Extensions**.

## 1.5.0
- **Install with no Python and no commands.** Claude Desktop users install `aw-schedule-manager-1.5.0.mcpb` with a
  double-click. Claude Code users install from the marketplace as before; the plugin now runs a ready program, so
  Python is no longer needed.
- Claude Desktop settings: **Read only** switch and an optional **P6 database file** picker.
- New licence agreement (`LICENSE`) and third-party notices.

## 1.4.0
- `create_calendar`: new calendars with work days, hours with breaks, holidays and yearly holidays.

## 1.3.0
- `create_baseline`: save a copy of a project as its baseline, and assign it.

## 1.2.0
- 36 new tools: reports (DCMA 14-point check, critical path, cash flow and S-curve, baseline variance, resource
  summary, lists of WBS, calendars, resources, codes, UDFs and relationships) and editing (many activities at once,
  progress updates in one step, data date, WBS, relationships, activity codes, UDFs, notebooks, steps, expenses,
  baselines, project settings, resources and assignments).

## 1.1.1
- Editing stays off unless it is explicitly turned on.

## 1.1.0
- Browse for the database file with `choose_database`.
