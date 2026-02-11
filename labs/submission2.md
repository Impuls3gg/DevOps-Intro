# Lab 2 Submission

## Task 1

```bash
$ git log -1 --oneline
d191dc2 (HEAD -> main) Add test file

$ git cat-file -p d191dc2
tree 6fc34c927366108fc0b6754f0396379135ff7cea
parent 2c737e7744932694ae50fd999da41bf3984133f9
author Gadel Mahmutov <1mpulse77520@gmail.com> 1770830532 +0300
committer Gadel Mahmutov <1mpulse77520@gmail.com> 1770830532 +0300
gpgsig -----BEGIN SSH SIGNATURE-----
 U1NIU0lHAAAAAQAAADMAAAALc3NoLWVkMjU1MTkAAAAgDAHIGCOqFs2zaFQ+PHlkBwUGpY
 6iQP6YdkKVzDwZR00AAAADZ2l0AAAAAAAAAAZzaGE1MTIAAABTAAAAC3NzaC1lZDI1NTE5
 AAAAQEV1j/+DrMubU7omApdFM6wtWzoxuy1CA8j7NkmjZI3n/FXy1NtRXikUqaDLr6uj6a
 Ms7KubWCrfdO1gXrPihAI=
 -----END SSH SIGNATURE-----

$ git cat-file -p 6fc34c927366108fc0b6754f0396379135ff7cea
040000 tree f56a923600f205f02b01630b797640632b1680f5    .github
100644 blob 6e60bebec0724892a7c82c52183d0a7b467cb6bb    README.md
040000 tree a1061247fd38ef2a568735939f86af7b1000f83c    app
040000 tree eb79e5a468ab89b024bd4f3ed867c6a3954fe1f0    labs
040000 tree d3fb3722b7a867a83efde73c57c49b5ab3e62c63    lectures
100644 blob 2eec599a1130d2ff231309bb776d1989b97c6ab2    test.txt
100644 blob c57b1ca70fd9310aec2f9adfafa784fb169cab29    test_signature.md

$ git cat-file -p 6e60bebec0724892a7c82c52183d0a7b467cb6bb
# 🚀 DevOps Introduction Course: Principles, Practices & Tooling

[![Labs](https://img.shields.io/badge/Labs-80%25-blue)](#-lab-based-learning-experience)
[![Exam](https://img.shields.io/badge/Exam-20%25-orange)](#-evaluation-framework)
[![Hands-On](https://img.shields.io/badge/Focus-Hands--On%20Labs-success)](#-lab-based-learning-experience)
[![Duration](https://img.shields.io/badge/Duration-10%20Weeks-lightgrey)](#-course-roadmap)
```
Blob: Stores the raw contents of a file. It does not contain the filename or permissions, only the data itself.
Tree: Represents a directory. It maps filenames to blob hashes (files) or other tree hashes (subdirectories), along with file permissions.
Commit: A snapshot of the project at a specific point in time. It points to a root tree object and contains metadata such as the author, timestamp, message, and a pointer to the parent commit.
## Task 2
```bash
git reset --soft HEAD~1
```
The HEAD pointer moved back one commit. The changes from the undone commit were preserved in the Staging Area (Index). The file remained modified in the working directory.

```bash
git reset --hard HEAD~1
```

The HEAD pointer moved back. The changes were completely discarded from both the Staging Area and the Working Directory. The file reverted to its state from the previous commit.

```bash
$ git reflog
ed1db98 (HEAD -> git-reset-practice) HEAD@{0}: reset: moving to HEAD~1
34e31b7 HEAD@{1}: reset: moving to HEAD~1
20dd654 HEAD@{2}: commit: Third commit
34e31b7 HEAD@{3}: commit: Second commit
ed1db98 (HEAD -> git-reset-practice) HEAD@{4}: commit: First commit
d191dc2 (main) HEAD@{5}: checkout: moving from main to git-reset-practice
d191dc2 (main) HEAD@{6}: commit: Add test file
2c737e7 (origin/main, origin/HEAD, pr_template_test) HEAD@{7}: checkout: moving from feature/lab1 to main
85c2fbb (origin/feature/lab1, feature/lab1) HEAD@{8}: commit: docs: add lab1
8497158 HEAD@{9}: commit: test: pr template
bf1fe5c HEAD@{10}: checkout: moving from pr_template_test to feature/lab1
2c737e7 (origin/main, origin/HEAD, pr_template_test) HEAD@{11}: checkout: moving from main to pr_template_test
2c737e7 (origin/main, origin/HEAD, pr_template_test) HEAD@{12}: checkout: moving from test_pr_template to main
50beb95 (origin/test_pr_template, test_pr_template) HEAD@{13}: commit: test: verify PR template
2c737e7 (origin/main, origin/HEAD, pr_template_test) HEAD@{14}: checkout: moving from main to test_pr_template
2c737e7 (origin/main, origin/HEAD, pr_template_test) HEAD@{15}: commit: add PR template
fd43c2c HEAD@{16}: checkout: moving from test-template-2 to main
d0b3840 (origin/test-template-2, test-template-2) HEAD@{17}: commit: test: verify template again
fd43c2c HEAD@{18}: checkout: moving from main to test-template-2
fd43c2c HEAD@{19}: checkout: moving from main to main
fd43c2c HEAD@{20}: checkout: moving from feature/lab1 to main
bf1fe5c HEAD@{21}: commit: test: verify PR template works
fd43c2c HEAD@{22}: checkout: moving from main to feature/lab1
fd43c2c HEAD@{23}: commit: add PR template
dca72f9 HEAD@{24}: checkout: moving from main to main
dca72f9 HEAD@{25}: commit: docs: add commit signing summary
d6b6a03 HEAD@{26}: clone: from https://github.com/Impuls3gg/DevOps-Intro.git
```
## Task 3
```bash
$ git log --oneline --graph --all
* 5999eee (side-branch) Side branch commit
* ed1db98 (HEAD -> git-reset-practice) First commit
* d191dc2 (main) Add test file
| * 85c2fbb (origin/feature/lab1, feature/lab1) docs: add lab1
| * 8497158 test: pr template
| * bf1fe5c test: verify PR template works
| | * 50beb95 (origin/test_pr_template, test_pr_template) test: verify PR template
| |/
|/|
* | 2c737e7 (origin/main, origin/HEAD, pr_template_test) add PR template
|/
| * d0b3840 (origin/test-template-2, test-template-2) test: verify template again
|/
* fd43c2c add PR template
* dca72f9 docs: add commit signing summary
* d6b6a03 Update lab2
* 87810a0 feat: remove old Exam Exemption Policy
* 1e1c32b feat: update structure
* 6c27ee7 feat: publish lecs 9 & 10
* 1826c36 feat: update lab7
* 3049f08 feat: publish lec8
* da8f635 feat: introduce all labs and revised structure
* 04b174e feat: publish lab and lec #5
* 67f12f1 feat: publish labs 4&5, revise others
* 82d1989 feat: publish lab3 and lec3
* 3f80c83 feat: publish lec2
* 499f2ba feat: publish lab2
* af0da89 feat: update lab1
* 74a8c27 Publish lab1
* f0485c0 Publish lec1
* 31dd11b Publish README.md
```
## Task 4
```bash
git tag v1.0.0
git push origin v1.0.0
```
Tags are used to mark specific points in history as important, typically for releases (e.g., v1.0, v2.0). Unlike branches, tags are immutable.

## Task 5
```bash
User@WIN-0EH1MKMGOQT MINGW64 ~/Desktop/DevOps-Intro (git-reset-practice)
$ git switch -c cmd-compare
Switched to a new branch 'cmd-compare'

User@WIN-0EH1MKMGOQT MINGW64 ~/Desktop/DevOps-Intro (cmd-compare)
$ git switch -
Switched to branch 'git-reset-practice'
```

git switch: Dedicated purely to switching branches. It is safer than checkout.
git restore: Dedicated purely to restoring files in the working tree or index.
git checkout: A legacy command that overloads functionality (it can switch branches OR restore files depending on arguments). It is recommended to use switch and restore to avoid accidents and ambiguity.
## Task 6
Stars: Starring repositories helps bookmark interesting projects for future reference. It also signals to the community and maintainers that the project is valuable, helping it gain traction and contributors.

Following: Following developers creates a personalized feed of activity. It allows me to discover new open-source projects they contribute to and network within the professional developer community.