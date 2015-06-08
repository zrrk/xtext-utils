
---

This solution is somewhat complicated, but gives you maximum control.
It might be easier to just add Google Code repos as an remote in the git-svn enabled repo (created with `git svn init ...`) and the push directly from there.

---


This is what we did for the unittesting subproject; in a temporary workbench folder:

## Clone the new Git REPO ##

`git clone https://lcorneliussen@code.google.com/a/eclipselabs.org/p/xtext-utils.unittesting/ xtext-utils-unittesting`

## Clone the old SVN-Folder using Git-SVN ##

`git svn clone http://svn.codespot.com/a/eclipselabs.org/xtext-utils/subprojects/unittesting svn-imp -s --authors-file=../authors.txt`

This will abort, for each author that couldn't be found in the authors.txt.

After adding the required author, rerun `git svn fetch` within `svn-imp`.

The authors for Xtext-Utils so far are:
```
lcorneliussen@gmail.com = Lars Corneliussen <me@lcorneliussen.de>
lcorneliussen = Lars Corneliussen <me@lcorneliussen.de>
karsten.thoms = Karsten Thoms <karsten.thoms@itemis.de>
karsten.thoms@googlemail.com = Karsten Thoms <karsten.thoms@itemis.de>
karsten.thoms@gmail.com = Karsten Thoms <karsten.thoms@itemis.de>
voelter = Markus Voelter <voelter@acm.org>
(no author) = Unknown <unknown@example.org>
weise25@gmail.com = Stefan Weise <stefan.weise@itemis.de>
```

## Migrating the Trunk (or other "branches") ##

```
# add a remote for the git-svn based repo
xtext-utils-unittesting> git remote add svn-imp ../svn-imp

# fetch all changes
xtext-utils-unittesting> git fetch svn-imp

# "importing" on a branch-per-branch basis
xtext-utils-unittesting> git branch svn-import svn-imp/master 
```

Then push the new local branch to Google Code

`xtext-utils-unittesting> git push origin svn-import`

In our case we also want to restructure, so instead of importing directly, I chose to use a temporary branch, which can be removed, when the import is complete.

## Migrating Tags ##

In SVN there is no real notion of a _tag_; it is just a naming convention. When migrating to GIT, we want to use the real tags, which are technically just a _post-it_ on any commit.

Here we'll migrate the release tag for '0.9.0'.

```
# list remote branches:
svn-imp> git branch -r
  tags/0.9.0
  trunk
  xtext1

# then tag the ones you want
svn-imp> git tag 0.9.0 tags/0.9.0
```

```
xtext-utils-unittesting> git fetch svn-imp
...
 * [new tag]         0.9.0      -> 0.9.0
...

# then push the new tag to google...
xtext-utils-unittesting> git push origin --tags
```