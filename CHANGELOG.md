# Changelog

## 1.7.1
- **Fewer tokens, same features.** The tool list Claude reads at the start of every session is about a quarter smaller
  (descriptions halved): the rules every tool shares (F5/F9, dry runs, units, naming, where files go) are now said once in the
  server instructions instead of in each tool. Schemas no longer repeat empty defaults.
- Tool results are sent as compact JSON. Long lists start shorter (critical_path 60, list_relationships 100,
  find_activities 100, compare_projects 60, baseline_variance 80, run_sql 200 rows); every answer still gives the full count
  and limit can be raised.
- Faster edits: whether P6 is open is checked at most every 5 seconds instead of on every edit.
- A one-column .csv no longer fails to load in import_progress_from_excel and renumber_activities.

## 1.7.0
- **16 new tools for keeping a P6 database and its schedules in order** (103 tools in all). The tools that change many rows
  check first and have a dry run: `dry_run=true` is the default and nothing is written until you say `dry_run=false`.
  - **Audits (read only):** `update_trend` (finish date, float, critical activities and % complete across a series of updates),
    `logic_audit` (duplicate relationships, loops, redundant FS links, long lags, leads, SF links, links to LOE, activities with many
    links), `calendar_audit` (usage, same-name and look-alike calendars, calendars whose holidays run out), `resource_audit`
    (resources never assigned, without a price, with the same name, zero assignments), `activity_code_audit` (unused types and
    values), `database_health` (size, integrity, deleted rows still stored, ID counters, orphans, backup size) and
    `list_admin_categories`.
  - **Fixes:** `fix_logic` (remove exact duplicates and redundant FS links; different-type duplicates only on request, strongest kept),
    `renumber_activities` (replace text or regex, mapping, an Excel or CSV file, a UDF such as "New Activity ID", or a sequence; checks
    for duplicates and length), `update_calendar` (add or remove holidays, yearly holidays, worked days, rename, delete unused,
    many calendars at once with wildcards), `manage_resource_rates` (list, add, escalate by a percentage from a date, delete a price;
    optionally re-price open assignments), `purge_deleted` (remove rows deleted long ago and shrink the file; P6 must be closed),
    `edit_activity_code` (rename, merge duplicates, delete unused, copy a code to another project, assign by name or ID pattern),
    `global_change` (bulk edit of the activities that match conditions, like P6 Global Change), `edit_admin_category` (expense
    categories, units of measure, notebook topics, project phases, document categories and statuses, risk categories, currencies) and
    `copy_wbs` (copy a WBS branch with activities, relationships, resources, codes, UDFs and expenses, inside a project or into another).
- Reading a P6 calendar's holidays and working times works on the exact stored data, so changing holidays leaves every other
  exception and the work week untouched.

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
