# Homework 5: Current User, Logout, and GitHub Workflow [for credit]

This starter code is provided for CSC207 Summer 2026.

You are encouraged to use the [CAVE Learn Tool](https://ca-visualizer-for-education.github.io/cave-learn/) to learn and review Clean Architecture concepts while working on this homework. 

There is also a CAVE survey worth 0.5% at the bottom of this handout.

## Important notice about visibility of your GitHub repo
This homework is **individual work**. Every student should complete the coding
tasks in their own private GitHub repository and submit their own working solution.

Do **not** use GitHub's **Fork** button for this homework. Forks of public
repositories are public, and GitHub does not let you make them private.

Instead, create a new **private** GitHub repository and copy the starter code
into it. You must keep your repository **private** until further notice. The
teaching team will send an announcement after the latest extension deadline has
passed.

## Preamble

In this homework, you will work with a program designed using Clean Architecture.
The starter code includes complete signup and change password use cases,
and partially completed login and logout use cases.

You will also practice a lightweight GitHub issue/branch/pull request workflow **for credit**.
For this homework, the workflow is individual practice: you will create issues,
assign them to yourself, open pull requests in your own repository, leave
self-review comments, and merge into your own `main` branch. In the course
project, you will use the same workflow with real teammate reviews.

To summarize, during this assignment, you will:

- practice exploring and modifying a Clean Architecture codebase,
- add current-user tracking to the login use case,
- write or update a unit test for a use case interactor,
- complete the logout use case,
- practice using GitHub issues and pull requests, and
- keep your `main` branch in a testable state.

## Task 0: Create a private repository, clone it, and identify yourself

Create a new **private** GitHub repository for this homework under your own
GitHub account, then clone it. Do not use GitHub's **Fork** button. After
creating the private repository, copy the starter code into it, commit the
starter code, and push it to your private repository. Copy the project files
only; do not copy another repository's `.git` directory into your private
repository if you are using `git clone` to download the starter code from this public repo.

Open the project in IntelliJ and make sure you can successfully run `app/Main.java`.
You may need to set the Project SDK in the `Project Structure...` menu, and you
may also need to manually sync the Maven project.

MarkUs autotesting will be available later. If you want to run the MarkUs
autotests, you must upload your code to MarkUs. The student-run MarkUs tests
will run on the files you upload to MarkUs, not on your private GitHub
repository.

For the actual grading, including hidden GitHub workflow testing, you must submit
a link to your homework GitHub repository on MarkUs:

- Click **Submit Link** on the MarkUs submission page.
- In **URL**, enter the HTTPS URL of your HW5 GitHub repository, such as
  `https://github.com/your-github-account/csc207-hw5`.
- In **Display URL as**, enter `github`.

Do not submit an SSH URL such as `git@github.com:your-github-account/csc207-hw5.git`. This
is very important; otherwise, we may not be able to grade your Homework 5
submission.
Your MarkUs submission is how the teaching team will connect your GitHub
repository to you.

After the teaching team announces that you may make your repository public, your
Homework 5 submission will be graded.
Your issues, pull requests, `Self-review:` comments, and merges should all be completed before the deadline.

## Task 1: Understand the program

Open up `app.Main` and `app.AppBuilder`.

Discuss or think through these questions:

- What are the Views?
- What are the current use cases?
- Which use cases are triggered from each View?
- Which version of the DAO is `app.Main` using?
- Why do the `addX` methods in `AppBuilder` end with `return this;`?

Run the program and make sure the signup, login, and change password use cases work.
From the GUI, you should notice that the "Log Out" button does not actually log
the user out.

There is one more missing piece that is not directly visible from the GUI: the
login use case does not save who the current user is in the data access layer.
You will see this by reading the login interactor and DAO code, and you will
confirm it by writing a unit test.

You will fix both of these. But do not start yet, keep reading the handout!

### A short note on Java exceptions

While exploring the DAO code, you may see Java exception-related words such as
`Exception`, `IOException`, `RuntimeException`, `try`, `catch`, and `throws`.
An exception is Java's way of signalling that a method could not finish normally
because something unusual happened, such as a file or API call failing.

You do not need to write new exception-handling code for this homework. Also note
that ordinary use case failures, such as an incorrect password, are handled through
methods like `prepareFailView`, not by throwing exceptions.

## Task 2: Practice an individual GitHub workflow

The issue/branch/pull request workflow is a standard way for software teams to
collaborate, including small teams. In this homework, you will practice a
lightweight individual version of the workflow. The code is your own individual
work, but the habits are the same ones you will use with teammates during the
course project.

Some GitHub vocabulary for this homework:

- An **issue** is a GitHub page used to track a task, bug, feature, or question.
  In this homework, each issue should describe one small piece of your implementation.
  See GitHub's
  [introduction to issues](https://docs.github.com/en/issues/tracking-your-work-with-issues/learning-about-issues/about-issues).

- An **assignee** is the person responsible for working on an issue or pull request.
  To assign yourself to an issue, open the issue, find **Assignees** in the right
  sidebar, and choose your GitHub account. See GitHub's
  [instructions for assigning issues and pull requests](https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/assigning-issues-and-pull-requests-to-other-github-users).

- A **reviewer** is someone asked to look over a pull request before it is merged.
  In a real team workflow, you request a reviewer by opening the pull request and
  choosing a teammate in the **Reviewers** section on the right sidebar. GitHub then
  notifies that teammate. A reviewer can leave comments, approve the pull request,
  or request changes. See GitHub's
  [instructions for requesting a pull request review](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/requesting-a-pull-request-review).
  You are not required to request a reviewer for this individual homework.

- A **pull request**, often abbreviated as **PR**, is a request to merge changes
  from one branch into another branch. In this homework, your PR is how you show
  and check the code you wrote before merging it into your own `main` branch. See
  GitHub's
  [introduction to pull requests](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests).

- A **review comment** is a comment on a pull request or on a changed line of code.
  GitHub's formal review options are **Comment**, **Approve**, and **Request changes**.
  An approval is a special review state, not just an ordinary comment. For this
  individual homework, we will use a required regular comment beginning with
  `Self-review:` instead, so that everyone can complete the workflow in their own
  repository. You are not required to request or receive an approval. GitHub does
  not allow pull request authors to approve their own pull requests.

An optional reading about effective pull requests is available here:
[How to create effective pull requests](https://dev.to/mpermar/how-to-create-effective-pull-requests-2m8e).

Required workflow:

1. Create **at least these two required GitHub issues** in your repository:
   - one issue for current-user tracking in the login use case, and
   - one issue for completing the logout use case.
   
   You can also write one issue per TODO.

   If you do not see an **Issues** tab in your repository, enable issues in your
   repository settings.

2. Assign each issue to yourself using the **Assignees** section on the issue page.
   Each issue must briefly describe what the issue is about. We also recommend
   including:
   - the file or files you expect to edit,
   - the TODOs or behaviour you plan to complete,
   - the expected behaviour when the issue is done, and
   - any relevant test or manual check.

3. Create a branch for the current-user tracking issue. Use a short, descriptive branch name. It is often
   helpful to include the issue number. For example:
   `issue-1-current-user` or `current-user-tracking`.

4. Complete the code for the current-user tracking issue. Keep your branch focused on the issue. Avoid
   unrelated formatting, cleanup, or refactoring.

5. Open a pull request from your branch into your own `main` branch. Give it a
   short, specific title. In the pull request description, include:
   - which issue your pull request fixes,
   - a closing keyword such as `Fixes #1`, replacing `1` with the issue number,
   - which TODOs or behaviours you completed,
   - which files you changed,
   - a brief explanation of how your code works,
   - how you tested your change, and
   - anything you are unsure about.

   The closing keyword is important: when the pull request is merged into `main`,
   GitHub should automatically close the linked issue.

6. Assign the pull request to yourself using the **Assignees** section on the pull
   request page.

7. Leave at least one self-review comment on your own pull request before merging.
   This should be a regular comment, not a GitHub **Approve** review. Open the pull
   request's **Conversation** tab, use the comment box, and begin the comment with
   exactly `Self-review:`. For example:

   `Self-review: I checked that this PR fixes issue #1, updates LoginInteractor,
   and adds a login test for the current user.`

   In a real team, pull request comments are one of the main ways teammates
   communicate about code. They are used to ask questions, explain design choices,
   point out possible bugs, suggest changes, and record what was checked before
   merging.

8. Merge the pull request into your own `main` branch. Check that GitHub closed
   the linked issue, then run the relevant tests or manual checks on `main`.

9. Repeat the workflow for the logout issue. You should have at least two
   separate required pull requests: one for current-user tracking and one for
   logout.

Complete, add the `Self-review:` comment, merge, and test the current-user tracking
pull request before starting the logout pull request. The logout use case depends
on the DAO being able to remember the current user.

Do not enable branch protection rules that require an approving review for this
homework. GitHub will not let you approve your own pull request, and this homework
uses self-review comments only as individual workflow practice.

**Now, we can take a closer look at what you are supposed to do to fix the issues.**

## Task 3: Track the current user after login

The DAO does not currently keep track of which user is logged in. Add this behaviour
to the login use case.

Use the method names `setCurrentUsername` and `getCurrentUsername`.

1. In `LoginInteractor`, after the user has successfully logged in and before the
   `LoginOutputData` is created, save the current username in the data access object.

2. Add the needed current-user methods to `LoginUserDataAccessInterface`.

3. Update the implementing DAO classes so the program compiles. For this homework,
   the important implementation is `InMemoryUserDataAccessObject`, because `AppBuilder`
   uses the in-memory DAO.

   In `InMemoryUserDataAccessObject`, `setCurrentUsername` should save the username
   in an instance variable, and `getCurrentUsername` should return it. Use `null` to
   mean that nobody is currently logged in.

4. Update `LoginInteractorTest` by adding a test for login status. Name the new
   test method `successUserLoggedInTest`. The test should:
   - add a user to the DAO,
   - check that nobody is logged in before login with
     `assertNull(userRepository.getCurrentUsername())`,
   - execute the login use case for that user, and
   - check that the user is recorded as the current user with
     `assertEquals("Paul", userRepository.getCurrentUsername())`.

## Task 4: Complete the logout use case

We have created all the Clean Architecture classes necessary for the logout use case,
but some code is missing.

You will know you are done when:

- clicking the "Log Out" button takes the user back to the Login View,
- the current user in the DAO is set back to `null`, and
- the provided `LogoutInteractorTest` passes.

The logout TODOs are summarized below.

* * *

- `Main.java`

    - [ ] TODO: add the Logout Use Case to the app using the appBuilder
    - Hint: check how the other use cases were added.

* * *

- `LoggedInView.java` (tip: refer to the other views for similar code)

    - [ ] TODO: save the logout controller in the instance variable.
    - [ ] TODO: execute the logout use case through the Controller

* * *

- `LogoutController.java` (tip: refer to the other controllers for similar code)

    - [ ] TODO: save the interactor in the instance variable.
    - [ ] TODO: run the use case interactor for the logout use case

* * *

- `LogoutInputData.java` (should be done with the LogoutInteractor TODOs below)

    - [ ] TODO: save the current username in an instance variable and add a getter.

- `LogoutInteractor.java` (tip: refer to `ChangePasswordInteractor.java` for similar code)

    - [ ] TODO: save the DAO and Presenter in the instance variables.
    - [ ] TODO: implement the logic of the Logout Use Case

* * *

- `LogoutOutputData.java`

    - [ ] TODO: save the parameters in the instance variables.

* * *

- `LogoutPresenter.java` (tip: refer to `SignupPresenter.java` for similar code)

    - [ ] TODO: assign to the three instance variables.
    - [ ] TODO: have `prepareSuccessView` update the `LoggedInState`
    - [ ] TODO: have `prepareSuccessView` update the `LoginState`

## Testing and grading checks

This homework has three layers of tests/checks:

1. **Local self-tests** are available in `src/test/java`. These are a subset of
   the MarkUs autotests. You can run them in IntelliJ while working, or with
   Maven using `mvn test` if Maven is available on your machine. These tests are
   meant to help you check some of the main behaviours while you work.

   The main local self-tests for this homework are:
   - `use_case/login/LoginInteractorTest.java`, where you must add
     `successUserLoggedInTest`,
   - `use_case/logout/LogoutInteractorTest.java`, which checks that the logout
     interactor clears the current user, and
   - `use_case/signup/SignupInteractorTest.java`, which is available as an
     example of the testing style and as a check for starter code that was
     already working.

   The local self-tests do not check every required behaviour. For example, they
   do not fully check the GitHub workflow, view wiring, or all presenter updates.

   The starter code is incomplete, so some self-tests may fail or may not compile
   until you finish the required TODOs.

2. **MarkUs autotesting** will be available later. These tests are a larger set
   than the local self-tests, but they are still not the full grading suite. For
   example, they may check that logout is wired through the controller, view,
   presenter, and `Main.java`, and they may include style checking. To run these
   student-run MarkUs tests, upload your files to MarkUs; MarkUs does not access
   your private GitHub repository for self-testing.

3. **Full autotesting and grading** may include additional hidden tests.
   These checks are used for final grading. For example, your GitHub workflow
   will be checked. Make sure you submit your GitHub repository link on MarkUs
   and make the repository public when instructed to do so.

## Task 5: Final checks

Before submitting:

- run the local self-tests in `src/test/java`, especially the login and logout
  interactor tests,
- run the program manually and try signup, login, change password, and logout,
- make sure your final code is merged into your own `main` branch,
- once MarkUs autotesting is available, upload your code to MarkUs if you want to
  run the MarkUs autotests,
- submit your GitHub repository link on MarkUs using **Submit Link** for the
  GitHub workflow grade, and
- make sure your issues and pull requests show your individual workflow practice.

## CAVE Learn survey

As mentioned, this homework includes the first of two CAVE surveys about Clean Architecture.
This first survey is worth 0.5% of your final grade. Together, the two CAVE surveys are worth 1% of your final grade.

The first survey is due **Friday, July 10, 2026**:
[CAVE Learn Survey 1](https://q.utoronto.ca/courses/433013/quizzes/520521)
If you consent to complete the survey, you will be able to access the actual survey at [CAVE Survey #1 Redirect](https://q.utoronto.ca/courses/433013/pages/cave-survey-number-1-redirect).
Please ignore the mark you received for CAVE Learn Survey 1. The survey will be due at the same time as the homework (at 11:59 p.m on July 10).
If [CAVE Survey #1 Redirect](https://q.utoronto.ca/courses/433013/pages/cave-survey-number-1-redirect) is still not available after you give consent, please try refreshing the page or reach out to us.
