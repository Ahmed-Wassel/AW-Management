# Privacy policy

Effective 8 November 2026 (update check added in 1.5.1). This policy covers AW Schedule Manager by Ahmed Wassel, as a Claude Desktop extension and as a Claude Code plugin.

## Data collected

The software runs on your computer. The developer doesn't run a service for it, and receives no data from it. It has no accounts, cookies or analytics.

The software reads the P6 database you choose. That database can include personal data, such as the names and email addresses of resources and users.

## How data is used and stored

The software uses your data only to answer your requests and make the edits you approve. It stores data only on your computer:

- in your P6 database, when you approve an edit
- in backups taken before each edit, in `p6_backups\<database name>` next to the database
- in XER files you ask it to create
- the path of the database you chose: in the software's data folder (Claude Code), or in the extension settings or the `.aw-schedule-manager` folder in your user folder (Claude Desktop)

## Update check

The software connects to the internet only to check for updates, and only in two cases:

- when you ask Claude to run `check_for_updates`;
- if you turn on the **Check for updates** setting (off by default): then at most once a day.

The check asks GitHub (github.com, a service of GitHub, Inc.) for the latest release of AW Schedule Manager. The only information sent is the version number of the software you have, in the request header. Like any web request, GitHub sees your IP address; the developer receives nothing. The answer and the time of the last check are kept in the software's data folder on your computer. No project data is ever sent.

## Sharing

Apart from the update check above, the software sends data to no service. What a tool returns goes to Claude as part of your conversation, under your agreement with Anthropic. Check that sharing project data with an AI service is allowed by your company and contract.

## Retention

The developer retains nothing, because the data never reaches the developer. The software keeps the last 15 backups for each database, until you delete them. To remove them, delete the `p6_backups` folder. Your database and XER files stay until you delete them.

## Contact

Open an issue at https://github.com/Ahmed-Wassel/AW-Management/issues.
