# sptk-styleguide-git
*The Git styleguide of Spintank*

## Learn Git
[Codecademy](https://www.codecademy.com) has a great tutorial about Git.

## Starting a new project
- Create a GIT repo (see GIT syntax)
- Clone the starterkit repo adequate in your sites folder
- Rename the starterkit folder and delete the .git file

```bash
cd Sites/nameoftherepo
git init
git remote add origin https://github.com/Spintank/nameoftherepo.git
git push -u origin master
```

That's it!

## Workflow
- Pull changes from the remote
```bash
$ git pull
```
- Create a branch if you're working on a new feature
```bash
$ git branch branch-name
```
- Develop and write a nice commit
- Pull again (in case new commits were made while you were working)
- Push your branch to the remote
```bash
$ git push
```
- If you're merging to master, delete the branch you were working on
```bash
$ git branch -d branch-name
```

## About commits
- Start your commit with a verb (add, change, remove…)
```bash
$ git commit -m "add vendors"
```
- Commit after every major changes (new template or functionality)
- Make a branch for each big feature or version.
