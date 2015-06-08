# Repository Structure #

Each subproject is hosted in it's own git-repository; but within the same google code project.

There is no trunk, and there is no master! Always develop on a version-branch, eg. 0.9.x or later 1.x

Branches from versions that are not maintained anymore can be deleted, because they can easily be restored from any tagged version at any time.

```

unittesting
 branch 0.9.x -> Development of the current 0.9.1 ++

```

## New Features ##
New features should be developed in branches and then integrated to the main trunk-like version branch.

# Build #

Build is done using Eclipse Tycho: a fine maven plugin for Eclipse builds.

## Build and Deploy a new SNAPSHOT ##

Allthough we'd like to automate this soon; we haven't come so far yet.

Have a look at Build- and Deploy-steps in the Release Process. It is quite similar, just that you deploy to `releases/unittesting-<dev-branch-name>`. **Remember to also remove old jars, when updating with a new snapshot build**.

## Create and Deploy a new RELEASE ##

**Change version**

  1. Create a tmp-branch
  1. `mvn org.eclipse.tycho:tycho-versions-plugin:set-version -DnewVersion=<version>-SNAPSHOT`
-SNAPSHOT is used here, since the bundle versions should have .qualifier
  1. `mvn versions:set -DnewVersion=<version>`
This will set the POM versions to a release version
  1. Commit the changes

**Build**

  1. `mvn clean package -Prelease`

**Tag**

  1. Create a tag
  1. Delete tmp-branch

**Bump to development version**

  1. Back on the version branch, run
`mvn org.eclipse.tycho:tycho-versions-plugin:set-version -DnewVersion=0.9.1-SNAPSHOT`
  1. Manually adjust versions in `eclipse-repository/category.xml`
  1. Commit and Push
  1. Push the with `--tags`


**Deploy**

  1. (?) Clone the distribution-repository locally
  1. Grab the `./eclipse-repository/target/repository/*` and replace/create + commit + push `releases/unittesting-<dev-branch-name>`
  1. after about 10 to 15 minutes, it will be available at http://xtext-utils.eclipselabs.org.codespot.com/git.distribution/releases