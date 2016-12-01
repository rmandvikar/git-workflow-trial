# git-workflow-trial
git workflow trial


## Branches:

Since the branches are public, any merge is always no fast-forward (--no-ff).

`stg` is most ahead and contains work commits. It points to STG environment.
`master` is the code in PRD environment.
`last` is the previously deployed code to PRD and `next` is the code to be 
deployed during next release.
`dev` is not shown intentionally but it points to dev environment.

```
stg     // represents staging
next    |
master  | these branches are away by 1 merge commit typically
last    |
```

Look at the Network tab (Graphs -> Network) for a repo graph.


## Release:

```
git checkout last
git merge master --no-ff

git checkout master
git merge next --no-ff

git checkout next
git merge stg --no-ff
```


## Hotfixes:

`hotfix` branches are branched from `master` and later merged into it similarly.
They are also merged into `next` and `last`.

```
// temporarily freeze master so it does not move ahead.
git checkout -b hotfix1 master
// hotfix work
git checkout master
git merge hotfix1 --no-ff
// if a merge conflict then bring in master to hotfix1 branch and then merge.

// merge master (or hotfix branch) into next, stg, and dev.
```


## Feature branches:

Devs typically branch off from `master` but could also from `next` or `stg` or 
even a `feature` branch.
