[[Lerndokus bei Puzzle]]
[[All IT Ninjas]]
[[All Project Notes]]
[[All ToDo's]]



MailTrap auf int und lokal zum testen (kostenlos biss zu 200mails a day)
tests kannst du bis zum versenden schicken
Du kannst auch über die konsole mailen 



![[Pasted image 20250820113938.png]]

![[Techtalk Delayed_job.pdf]]





















































Bei jedem Merge auf den Main Branch wird die Code Qualität in Sonar Cube aktualisiert.
Die aktuelle Codequality soll in einer Pipeline auf SonarCube gepushed werden.


```yml
name: Build  
  
on:  
  push:  
#    branches:  
#      - main  
#  pull_request:  
#    types: [opened, synchronize, reopened]  
  
jobs:  
  build:  
    name: Build # Comment  
    runs-on: ubuntu-latest  
    steps:  
      - uses: actions/checkout@v2  
        with:  
          fetch-depth: 0  # Shallow clones should be disabled for a better relevancy of analysis  
      - name: Set up JDK 21  
        uses: actions/setup-java@v1  
        with:  
          java-version: 21  
      - name: Build and analyze  
        run: mvn clean install sonar:sonar -Dsonar.token=${{ secrets.SONAR_TOKEN }}

```





Sprint 1

Miguel 7
Nevio 4 = ill for 1.5 days only would have added 2
Janis 5
Manu 2 = okr pain
Livio 1 = ill but would have only added 2













	# PCTS Tool

[](https://github.com/puzzle/pcts "Git repository")

# [General Guidelines](https://puzzle.github.io/pcts/development/gen_guidelines.html#general-guidelines)

Some general guidelines for contributing to this project.

## [Code of Conduct](https://puzzle.github.io/pcts/development/gen_guidelines.html#code-of-conduct)

Check out our code of conduct [here](https://github.com/puzzle/pcts?tab=coc-ov-file).

## [Git Messages](https://puzzle.github.io/pcts/development/gen_guidelines.html#git-messages)

Use [conventional commits](https://www.conventionalcommits.org/en/v1.0.0/#summary) with the following types: `build`, `chore`, `ci`, `docs`, `feat`, `fix`, `refactor`, `revert`, `style`, `test`

### [Format](https://puzzle.github.io/pcts/development/gen_guidelines.html#format)

Each commit message should consist of a **type**, an optional **scope**, a **subject** and an optional **issue number**.

```text
type(scope): subject #issue-number
```

### [Types](https://puzzle.github.io/pcts/development/gen_guidelines.html#types)

The type should answer the Question 'What kind of change was made?', e.g. a fix or a new CI workflow.

The type must be one of the following:

- `feat`: A new feature in the software the user uses
- `fix`: A bug fix in the software the user uses
- `docs`: Documentation only changes
- `style`: Changes that do not affect the meaning of the code (white-space, formatting, ...)
- `refactor`: A code change that neither fixes a bug nor adds a feature
- `test`: Adding missing tests or correcting existing tests
- `build`: Changes that affect the build system or external dependencies
- `ci`: Changes to CI configuration files and scripts
- `chore`: Other changes that do not modify source or test files
- `revert`: Reverts a previous commit

### [Scopes](https://puzzle.github.io/pcts/development/gen_guidelines.html#scopes)

The scope should answer the question 'Where in the codebase was the change made?', e.g. in the API or in the authentication module.

Scopes are more fluid than types and are thus not handled as strictly. Some example scopes are:

- `overview`: A specific part of the frontend
- `shared`: Shared services or components
- `api`: Changes in a DTO or controller
- `service`: Changes in some validation or business service
- `persistence`: Changes in a persistence service
- `db`: Anything related to database schemas or migrations
- `deps`: Dependency updates

### [Git Messages Examples](https://puzzle.github.io/pcts/development/gen_guidelines.html#git-messages-examples)

- `feat: Allow users to upload a profile picture`
- `fix(api): Correctly handle null values in user endpoint #123`
- `docs: Update README with setup instructions #45`
- `chore(deps): Upgrade project dependencies #78`

## [Git Branching](https://puzzle.github.io/pcts/development/gen_guidelines.html#git-branching)

- Branches should be written in lowercase characters, hyphens and numbers.
- Each branch should also have a prefix like this `feature/`, `bug/`, ... .
- If a branch is connected to an issue, the issue number should be included after the prefix. For example `feature/1829-...` for the issue 1829.

### [Prefix](https://puzzle.github.io/pcts/development/gen_guidelines.html#prefix)

The prefix should be one of the following:

- `feature`: A new feature in the software the user uses or everything that cannot be placed under another category
- `bug`: A bug fix in the software the user uses
- `docs`: Documentation only changes
- `renovate`: Reserved for the Renovate bot

### [Git Branching Examples](https://puzzle.github.io/pcts/development/gen_guidelines.html#git-branching-examples)

- `bug/1571-inconsistent-auto-calculation-on-metric-keyresults`
- `feature/18-create-member-view`
- `bug/remove-wrong-reference` (this branch does not have an associated ticket)
- `docs/12-add-missing-db-setup`

## [Pull Requests (PR)](https://puzzle.github.io/pcts/development/gen_guidelines.html#pull-requests-pr)

- **PR description:** Add any needed additional context to the PR description.
- **Mark your PR as a draft:** If the PR is not yet ready for a review, mark it as a draft.





















Validaten einbauenn 
und wengen error keys schauen 
rebase



7:30

12:00
12:50

17:15