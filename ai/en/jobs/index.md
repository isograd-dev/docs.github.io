---
layout: admin-manual
---

# Skill profiles

A **skill profile** (sometimes called a "job profile") is a benchmark of expectations: for a given job (for example *Administrative assistant*, *Junior accountant*, *Project manager*), you define **the expected level of mastery for every skill evaluated** by the Tosa subjects. A candidate's results can then be **compared** to this profile to visualise, skill by skill, the gap between expected and observed.

Open this page through the **Parameters → Expected Outcomes** menu.

![Main "Profiles management" page](img/01-liste-profils.png)

The **Manage Profiles** page lists every profile defined on your account. Each row shows the identifier (**ID** column) and the profile name (**Profile List** column); clicking a column header sorts the list. The **Add a Profile** button creates a new profile and the **pencil** button opens the expected levels configuration page.

Two tools complete the list:

- the **search** field of the filter panel finds a profile by its name or identifier;
- the **Export to Excel** button prepares an Excel file of the displayed list; then click on **Download** to retrieve it.

> 💡 **What is the practical use?** — Once a profile is defined, you can assign it to a candidate (or a group). When the candidate takes their tests, the generated report automatically compares their scores to the levels expected by the profile, and highlights the skills below the threshold. It is the reference tool for **strategic workforce planning** or **skills management** initiatives in a company.


## Create a profile {#create-a-profile}

1. From the **Manage Profiles** page, click on **Add a Profile** in the action bar.

    ![Profile add window](img/02-modal-ajout.png)

2. Enter the **Description** of the profile (mandatory field) — this is the name that will appear in the list and will be used for the assignment to candidates. Choose a meaningful label ("Junior accounting assistant", "Frontend web developer").

3. Click on **Save**. The profile is created and you are automatically redirected to its expected levels configuration page — see [Define required levels](#define-required-levels).


## Define required levels {#define-required-levels}

This is the central step: for each combination of **profile × language × subject**, you specify the expected level on each of the skills ("domains") evaluated by the subject.

![Page "Edit required levels"](img/03-page-niveaux.png)

The **Edit required skill levels** page is organised into two zones:

1. **Selection banner**:
    - **Job** — the profile being edited (read-only).
    - **Language** — the language of the subjects offered. Changing the language reloads the page with the list of subjects of that language: save your modifications first.
    - **Subject** — the topic to configure (Word, Excel, Python, English, etc.). The list has a search field; the table is updated as soon as a subject is chosen.
2. **"Skill Requirements Per Profile" card** — the table of skills to configure for the selected subject.

### Reading the skills table

![Skills table](img/04-tableau-competences.png)

The table has **three columns**:

- **Skill** — name of the evaluated skill domain (for example *Tables and queries*, *Forms and reports*, *Calculation functions*).
- **Required Level** — a number flanked by two **−** and **+** buttons. This is the expected level for this profile on this skill. It ranges from 1 to the highest level of the skill; as long as you have saved nothing for a subject, every skill is offered at level 3.
- **Description** — description of the skills evaluated at this specific level. The text updates automatically when you change the level, helping you calibrate the desired threshold.

To adjust a level, click on **+** to increase or **−** to decrease. The corresponding description is displayed in real time on the right.

### Save

Once the table is adjusted, click on **Save** — at the bottom of the table or in the bar at the top of the page, both buttons have the same effect — to persist the configuration. The save applies to the **subject currently selected**.

The bar at the top of the page also offers **Back to list** and, when you come from the profile list, the **Previous** and **Next** buttons to move to the neighbouring profile without going back through the list.

> 💡 **Working on several subjects** — To configure the same profile on several subjects, **always save before changing subject or language**. Switching subject or language without having saved would lose your modifications.

> ⚠️ **Subjects without skills** — Some subjects are not broken down into skills (for example, certain legacy tests or single-question tests). If you see the message *"There is no skill list defined for this subject."*, choose another subject; this subject is not configurable per profile.


## Edit an existing profile {#edit-a-profile}

1. On the **Manage Profiles** page, locate the profile's row and click on the **Edit** icon (pencil).
2. You land on the **Edit required skill levels** page. Adjust the levels on each subject (see [Define required levels](#define-required-levels)).
3. To change the **name** of the profile (its description), you will have to recreate it: the description cannot be modified directly after creation.


## Delete a profile {#delete-a-profile}

1. On the profile's row, click on the **Delete** icon (trash can).
2. A confirmation window appears.

    ![Deletion confirmation](img/05-confirmation-suppression.png)

3. Confirm. The profile is deleted.

### Profile already assigned to candidates

For a profile that is assigned to no candidate and on which no level is defined, the window simply asks *"Permanently delete this profile?"*. Otherwise, it **displays a warning** suited to the situation, followed by *"Delete anyway?"*:

- *"This profile is currently assigned to one or more candidates."*
- *"You have defined skill levels for this profile."*
- *"This profile is currently assigned to one or more candidates and you have defined skill levels for this profile."*

Deletion remains possible — it simply detaches the profile from the affected candidates. Their historical results are not affected, but future comparisons will no longer be able to use this profile. Confirm if you wish to clean up, or cancel if you first want to transfer the candidates to another profile.

> 💡 **Best practice** — Before deleting a profile in use, create its **replacement** and **reassign** the candidates to the new profile. This prevents the candidates' history from referencing a profile that no longer exists.
