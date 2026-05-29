---
layout: question-manual
---

# Tests (test forms)

A **test** — technically called a *"test form"* (`test_form`) in the code and audit reports — is the final assembly that becomes passable by a candidate. It is the junction point where you take a **selection of questions** from a subject, apply a **drawing algorithm**, set **parameters** (duration, number of questions, proctoring, etc.), and obtain a deliverable usable by a client account.

Every test booked for a candidate on the platform — whether an assessment, a certification or a positioning test — is defined by one of these forms.

Open the page through the menu **Questions module → Tests & Exams**, or directly at `/testforms/AdminTestFormsWithTable`.

![Tests management page](img/01-liste-formulaires.png)

The table (titled **TEST MANAGEMENT**) lists every test, with its **identifier**, **name**, **subject**, **language**, **type**, **algorithm** and **geographic visibility** (Worldwide by default, or restricted to certain countries/regions).


## Concepts {#concepts}

### Form types

Each form has a **type** (`typ_id`) that determines its purpose:

| Type | Use |
|---|---|
| **Assessment** | Continuous-assessment test, without certifying value. The most common format. |
| **Certification** | Test that officially sanctions a level. Subject to France Compétences rules if CPF-eligible. |
| **Proprietary certification** | Certification variant with account-specific rules. |
| **Subject-less certification** | Cross-cutting certification that is not attached to a specific subject. |
| **Positioning** | Diagnostic test taken at the start of a training course to assess the initial level. |

The type drives the platform's behaviour both on the candidate side (presentation, diploma generation) and on the administrator side (taking restrictions, available options).

### Drawing algorithm

A form does not directly contain the list of questions to ask — it defines **an algorithm** that selects questions at the start of each session. Common algorithms:

- **Adaptive** — the algorithm adjusts question difficulty based on the candidate's answers. This is Tosa's flagship algorithm.
- **CEFR / level** — targeted selection of a reference level (A1–C2 for languages).
- **Simple draw** — N questions drawn at random from a pool.

Each algorithm has its own parameters (length, domain pool, level distribution) configured on the **Algorithm** tab.

### Advanced mode vs client mode

The form's interface switches between two modes depending on privileges and context:

- **Advanced mode** (used by Isograd content teams) — 6 tabs, all editorial and technical options.
- **Client mode** — simplified 4-tab interface for account administrators who customise an existing form.

The mode is determined by the form's `is_advanced_test_form` flag and by your user profile.


## Create a test {#create-a-test}

Creation goes through a pre-selection modal (subject, language, type), followed by the edit page.

1. From the **Test forms management** page, click **Create a form** in the action bar.

    ![Creation modal](img/02-modal-creation.png)

2. Choose:

    - **Subject** — the topic the form assesses.
    - **Language** — language presented to the candidate.
    - **Type** — Assessment, Certification, etc. (see [Form types](#concepts)).

3. Confirm. The platform creates the form and takes you to its edit page.


## Tabs — advanced mode {#tabs-advanced-mode}

The edit page (titled **CREATE OR EDIT A TEST**) offers five tabs in advanced mode:

![Edit-page tabs in advanced mode](img/03-onglets-avance.png)

| Tab | Content |
|---|---|
| **General characteristics** | Public test (Yes/No), Geographic visibility, Active status, Brand, Main test for the subject family, Test type, plus the start and end messages shown to the candidate. The page also embeds a statistics panel (number of takes, ratings on relevance and ergonomics). |
| **Description** | Commercial descriptions per language: short card, long description, short description. Reused in public catalogues. |
| **Algorithm details** | Algorithm choice and parameters: assessed-domain pool, level distribution, drawing constraints, balancing of questions per domain. |
| **Results** | Analysis configuration: level thresholds, scoring formula, report structure. |
| **Other parameters** | Remote proctoring, full screen, automatic save, behaviour on interruption, miscellaneous technical options. |

> 💡 **Action buttons** — In addition to the **Save** button, the header offers **Save & try your test** (launches the test for yourself as a preview) and **Export comments** (retrieves the comments left by candidates on the questions of this test).

> 💡 **Lite mode** — In some environments (`is_cus_env`), the **Description** tab is not shown separately: its fields are inlined inside the **General characteristics** tab.


## Tabs — client mode {#tabs-client-mode}

For a client-account administrator who customises a form provided by Isograd, the interface is simpler:

| Tab | Content |
|---|---|
| **General** | Editable parameters: local name, status, subject (read-only). |
| **Time** | Test duration (can be adjusted locally). |
| **Intro & Feedback** | Customisation of intro and end messages. |
| **Statistics** | Summary table of the form's takes on this account. |

> 💡 **Why this restriction?** — In client mode, you **cannot** change the algorithm or the question pool, because those parameters are controlled by Isograd to guarantee consistent results across every account using the same form. You can, however, customise the **wrapping** (intro, feedback, duration).


## Edit a test {#edit-a-test}

1. On the form's row, click the **Edit** icon (pencil).
2. Navigate between the tabs and adjust the desired values.
3. Click **Save** at the top right.

> ⚠️ **Forms in production** — Editing a form **already used** by active candidates can affect their experience. For deep changes (algorithm, structure), prefer creating a **new form** or **duplicating** the existing one to keep a record of the historically used version.


## Duplicate a test {#duplicate-a-test}

Duplication is the fastest tool for creating a variant of an existing form (another language, a local adjustment, a "lite" version).

1. On the row of the form to duplicate, click the **Duplicate** icon.
2. The platform creates a copy with the "(copy)" suffix and takes you to its edit page.
3. **Rename** the copy to avoid confusion and adjust the parameters.

> 💡 **Duplication preserves** — the algorithm selection, proctoring parameters, descriptions, intro and feedback messages. It does **not** duplicate the **questions** themselves (forms reference them by filter, not by fixed list).


## Delete a test {#delete-a-test}

1. On the form's row, click the **Delete** icon.
2. Confirm on the confirmation page.

> ⚠️ **Form used by candidates** — A form referenced by **test bookings** (completed or in progress) cannot be deleted. Prefer **archiving** through the status field on the General tab: the form becomes invisible to new bookings but remains functional for historical tests.


## Filters {#filters}

The **Filters** panel offers:

- **Search** — free text on the name or the ID.
- **Language** — by form language.
- **Subject** — by associated subject.

Column sorting is available by clicking the headers.


## Authorise a test for an account {#authorize-test}

On the list, in addition to the **Create** button, you will find an **Authorise** button that opens an interface to grant an existing form to one or more **client accounts**. This operation controls access:

- The form becomes visible and usable by the targeted accounts.
- Other accounts do not see it in their selections.

Useful for proprietary forms ordered by a specific client, or for pilot certifications aimed at a restricted user group.


## Export the list {#export-the-list}

The **Export to Excel** button in the action bar generates an `.xlsx` file listing every form currently filtered. Valuable for periodic test catalogue reviews.
