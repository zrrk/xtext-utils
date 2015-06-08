# Introduction #

In xtext-utils it should be normal to create small subprojects for each use case. This small guide explains what steps must be done.

## Create Git Repository ##
  1. Go to [Administer/Source](http://code.google.com/a/eclipselabs.org/p/xtext-utils/adminSource).
  1. Click the _New respository_ link, enter the project name, check _Clone contents of_ and select `subproject-template`.
  1. Press enter to create the repository.

## Issue Tracker ##
  1. Go to [Administer / Issue Tracking](http://code.google.com/a/eclipselabs.org/p/xtext-utils/adminIssues)
  1. In _Predefined issue labels_ add a line
```
Component-<projectname>     = Issue relates to component '<projectname>'
```

To be continued...