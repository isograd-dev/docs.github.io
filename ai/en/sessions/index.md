---
layout: admin-manual
---

# Test session management

A **test session** is a time window (start date and time, end date and time) during which your candidates may start their test. It is the main tool to **frame** a test: proctored in person, scheduled on a precise slot, or simply protected by a code shared on the day.

![Main "Session management" page](img/01-liste-sessions.png)

The **Test session management** page lists all the sessions defined on your account. Each row shows the **ID**, the **name**, the **start date**, the **end date** and the **session code** (if any). If live proctoring is available on your account, a **Live proctoring** column flags live-proctored sessions with a camera icon. A **Paused** pill next to the name indicates a [paused](#pause-and-resume-a-session) session.

> 💡 **Default display** — The platform displays by default the **current** sessions and those **ended less than 3 months ago**. Older sessions remain in the database but are hidden from the list. The display options at the bottom of the filter panel let you include older sessions or hide past sessions.


## What is a session for {#what-is-a-session-for}

When you register a candidate to a test, you can **associate them with a session**. The consequences:

- The candidate can **start** the test only within the session's time window. Before the start date, the test appears but remains locked; after the end date, it is no longer accessible.
- If the session has a **code**, the candidate must enter it to start their test — the examiner communicates it at the appropriate moment, which adds a layer of security against premature starts.

You can also **assign an entire group** to a session in a single action from the **Candidate management** page (see [Group actions](/ai/en/candidates/#manage-groups)). This is the usual way to organize an examination day for a class or a training session.

> 💡 **Without a session** — A registration **without a session** means the candidate can start their test at any time once they have received their invitation. Sessions are therefore only useful if you want to **frame** the attempt in time.


## Create a session {#create-a-session}

### Procedure

1. From the **Test session management** page, click **Create a session** in the action bar.

    ![Session creation form](img/02-formulaire-creation.png)

2. Fill in the fields:

    - **Description** — label that will appear in the list (column *Session name*) and in the candidate registration form. Choose a meaningful name ("Promotion 2026 — session of 03/14").
    - **Session code** (optional) — password that the candidates will have to enter to start their test. To be communicated **only on the day of the session**. The regeneration button to the right of the field suggests a random code.
    - **Start date** and **End date** — window during which the tests attached to this session can be started. Enter using the `DD/MM/YY HH:MM` format.
    - **Live proctoring** (switch, optional) — only shown if your account uses Isograd remote proctoring. Turn it on so that proctors can follow the candidates' camera and screen **in real time** during the session (see [Live proctoring](/ai/en/proctoring/#live-proctoring)). Two fields then appear:
        - **Proctoring profile** (mandatory) — an Isograd remote proctoring profile **with video recording**. This profile is **imposed on every test** registered on the session.
        - **Proctors** — the administrators of the account holding the *Proctor test sessions live* privilege, who will be able to enter the session's meetings.

3. Click **Save**. The session appears immediately in the table.

> 💡 **Proctoring profile of a session** — Outside live proctoring, a session does not impose a proctoring profile: the profile is chosen **when registering** the candidate to the test (or through the *Assign a session or a proctoring profile* group action). If the **Live proctoring** switch is greyed out, no compatible profile exists yet: first create an Isograd remote proctoring profile with video recording.

> ⚠️ **Consistent dates** — The platform checks that the end date is after the start date and that the format is valid. An incorrect entry displays a message at the top of the form; the session is not created until the fields are valid.


## Edit a session {#edit-a-session}

1. On the session's row, click the **Edit** icon (pencil) at the end of the row. The edit window opens, pre-filled with the current values.

2. Adjust the desired fields (name, code, dates, live proctoring and its proctors).

3. Click **Save**.

### Notification of registered candidates

If the session already has registered candidates and you change the dates, the platform **automatically** offers to send a notification email to the affected candidates:

![Candidate notification window](img/03-modal-notification.png)

- **Yes** — sends an email to all candidates registered to the tests attached to this session, informing them of the new slot.
- **No** — the session is modified silently, with no email.

> 💡 **When to notify?** — Always notify if you **bring forward** the date or if you **shorten** the window — the candidates must be informed. For a simple **postponement** of a few minutes or a minor adjustment, you can choose not to send an email to avoid flooding inboxes.


## Pause and resume a session {#pause-and-resume-a-session}

An unexpected event during an exam (network outage, evacuation, incident in the room) may force you to **temporarily interrupt** all the candidates of a session. Rather than changing the dates or resetting each test, you can **pause the session**, then **resume** it while giving the lost time back to the candidates.

![Session in progress with the "Pause" button](img/06-session-en-cours.png)

The **Pause** button (pause icon) only appears at the end of the row for a session **in progress**, that is between its start date and its end date, and only if you have the write privilege on sessions.

### Pause

1. On the row of the session in progress, click **Pause**.

    ![Pause confirmation](img/07-modal-pause.png)

2. Confirm. From that moment, candidates taking a test of this session are **blocked**: their answers are no longer taken into account and they see a *"Session paused"* message. No candidate of the session can start or resume a test while the pause lasts.

    ![Paused session](img/08-session-en-pause.png)

The **Paused** pill is displayed next to the session name and the button becomes **Resume the session** (play icon).

### Resume

1. On the row of the paused session, click **Resume the session**.

    ![Session resume window](img/09-modal-reprise.png)

2. The resume window sums up what will happen to the **started** tests:

    - Started **TOSA certifications** are automatically **credited with the exact duration of the pause**; this value cannot be changed.
    - For the **other started tests**, the **Minutes to add to the other started tests** field is pre-filled with the duration of the pause; adjust it if needed (for example to grant a few minutes to settle back in).
    - Tests whose timer stops by itself during an interruption are not affected.

3. Confirm. The session resumes, candidates can go on and a message shows how many started tests were given extra time.

> ⚠️ **Session expired during the pause** — If the session's end date passed during the pause, resuming is refused: **first change the end date** of the session, then resume it.

> 💡 **Pause or stop a single test?** — The pause applies to **all** the candidates of the session. To interrupt a single candidate, use the **Stop the test** button on their registration record (see [The planned tests table](/ai/en/candidates/#the-planned-tests-table)).


## Delete a session {#delete-a-session}

### Delete a single session

1. On the session's row, click the **Delete** icon (trash can).

    ![Delete confirmation](img/04-confirmation-suppression.png)

2. Confirm. The session is deleted immediately.

The tests that were associated with this session remain registered to the candidates — they simply become **without a session**, and therefore startable at any time. If you also want to delete these tests, see [Delete tests from past sessions](#delete-tests-past-sessions) below.

### Delete multiple sessions at once

1. Check the boxes at the start of the row to select the sessions to delete.
2. Click **Delete the selected sessions** in the action bar.
3. Confirm. All the checked sessions are deleted in one operation.

> ⚠️ **Permanent deletion** — As everywhere on the platform, deletion is irreversible. To keep the history of a past session without seeing it in the list, simply let it age: beyond 3 months after the end date, it automatically disappears from the default display.


## Import multiple sessions {#import-sessions}

The import allows you to create several sessions in a single operation from an Excel file — useful at the start of the year to enter the entire exam calendar.

### Procedure

1. From the action bar, click **Import a session file**.

    ![Import window](img/05-modal-import.png)

2. Click the **Download the template** link to retrieve the expected Excel file. The template contains an `Import` sheet with the columns:

    | Column | Description |
    |---|---|
    | `des` | Session name |
    | `psw` | Session code (optional) |
    | `dat_sta_day`, `dat_sta_month`, `dat_sta_year`, `dat_sta_hour`, `dat_sta_min` | Start date, split into columns |
    | `dat_end_day`, `dat_end_month`, `dat_end_year`, `dat_end_hour`, `dat_end_min` | End date, split into columns |

3. Fill in the template, one session per row.

4. Come back to the platform, click **Choose a file** in the import window, select your filled-in Excel, then confirm.

5. The platform displays a report listing the sessions created, updated or rejected with their reason.

> 💡 **Update vs creation** — If a session in the file has the **same name** as an existing session, its dates and code are **updated** rather than a duplicate being created. This is convenient for re-importing a corrected file.


## Delete tests from past sessions {#delete-tests-past-sessions}

Over time, your account may accumulate **untaken tests** attached to sessions whose end date has passed. The platform exposes a bulk action to clean them up at once.

1. Click **Delete tests from past sessions** in the action bar.
2. Confirm. All **pending** tests (never started) whose session has ended are unregistered from the affected candidates.

> ⚠️ **Scope** — This action does **not** touch tests that have been **started**, **completed** or **cancelled**. Nor does it touch the sessions themselves — only the pending test registrations that were attached to them. The credits consumed at registration are returned to the account.


## Filters and display {#filters-and-display}

The **Filters** panel to the left of the list offers several settings to target which sessions to display:

- **Search** — free text. Filters the list on the session name or code.
- **Do not display past sessions** — hides all sessions whose end date is before now. Useful during the year to only see upcoming sessions.
- **Display sessions ended more than 3 months ago** — disabled by default. Enable it to reveal the older history (for example to find a session from 6 months ago).

The table is **sortable**: click the column header to switch between ascending and descending sort. By default, sessions are sorted by **start date**, most recent first.
