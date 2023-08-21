---
title:  "Git & Version Control"
date:   2023-08-03
categories: lewagon
---
Version control is a system that helps programmers manage changes to their code over time. It provides a structured approach to track modifications, additions, and deletions made to a project's source code, allowing developers to keep a detailed history of their work.

Git, specifically, is a popular and widely used distributed version control system. It offers a robust set of features for managing code repositories.

Git provides a rich set of commands that allow developers to interact with the version control system and manage their code repositories :

- git init: initializes a new Git repository in the current directory, creating the necessary metadata and data structures to start version controlling the code.
- git clone (repository): creates a local copy of a remote repository, allowing you to start working on it and keep it synchronized with the remote version.
- git add (file): adds a file to the staging area, preparing it to be committed in the next Git snapshot. Use git add . to add all modified files in the current directory.
- git commit -m "message": creates a new commit, which represents a snapshot of the code at a specific point in time. The -m flag allows you to provide a descriptive
message for the commit.
- git status: displays the current state of the repository, including modified files, files in the staging area, and untracked files.
- git log: shows a history of commits in reverse chronological order. It displays commit IDs, authors, timestamps, and commit messages.
- git diff: shows the differences between the working directory and the staging area. Use git diff --stagedto see the changes between the staging area and the last commit.
- git branch: lists all existing branches in the repository. The current branch is indicated by an asterisk (*).
- git checkout (branch): Switches to a different branch, allowing you to work on a separate line of development. Use git checkout -b (new-branch) to create and switch to a new branch.
- git merge (branch): combines the changes from a different branch into the current branch. It integrates the commit history and resolves any conflicts that may occur.
- git pull: fetches changes from a remote repository and merges them into the current branch. It's commonly used to update the local copy with the latest changes from the remote.
- git push: uploads local commits to a remote repository, updating the remote copy with your changes.
