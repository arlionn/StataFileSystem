---
layout: page
title: about
permalink: /about/
---

# Stata File System 
This is a program that allows users to access file system properties directly from their Stata session using a Java plugin.  The examples below are slightly out of date, but the program will now print an additional line in the display table with the name of the file owner, and the file owner will also be returned in the macro `r(fileowner)`.

A Stata program to access and modify file system properties.  Currently, the program/plugin allow users to:

1. Access file attributes 
2. Set the file to be executable globally or for the owner only
3. Set the file to be readable globally or for the owner only
4. Set the file to be writable globally or for the owner only
5. Make a file readonly protected

## Requirements
Plugin is compiled under Java 8.  Should not be a problem for most installations of Stata, but if you have an older JVM you can alter the JVM used by setting the appropriate properties.  To see the java property names use `query java`.

## Example 1. Get file attributes for the auto.dta data set and print them to the Stata console

```
. filesys `c(sysdir_base)'a/auto.dta, attr dis

----------------------------------------------------------------------------------------------------
    Attribute                File Attribute Value
----------------------------------------------------------------------------------------------------
    Created Date             20nov2015 05:44:54
    Modified Date            20nov2015 05:44:54
    Last Accessed Date       11dec2015 05:52:23
    Absolute File Path       /Applications/Stata/ado/base/a/auto.dta
    Canonical File Path      /Applications/Stata/ado/base/a/auto.dta
    Parent Path              /Applications/Stata/ado/base/a
    File Name                auto.dta
    Is Symbolic Link         false
    Is Regular File          true
    Is Executable            false
    Is Hidden                false
    Is Readable              true
    Is Writable              true
----------------------------------------------------------------------------------------------------

```

You can display the returned results afterwards as well.  

```
. ret li

macros:
         r(iswritable) : "true"
         r(isreadable) : "true"
         r(parentpath) : "/Applications/Stata/ado/base/a"
           r(ishidden) : "false"
           r(filename) : "auto.dta"
       r(isexecutable) : "false"
      r(canonicalpath) : "/Applications/Stata/ado/base/a/auto.dta"
        r(absoluepath) : "/Applications/Stata/ado/base/a/auto.dta"
           r(filesize) : "6443"
        r(regularfile) : "true"
            r(symlink) : "false"
        r(accessednum) : "1765432343000"
        r(modifiednum) : "1763617494000"
         r(creatednum) : "1763617494000"
           r(accessed) : "11dec2015 05:52:23"
           r(modified) : "20nov2015 05:44:54"
            r(created) : "20nov2015 05:44:54"
```

The `r(accessednum)`, `r(creatednum)`, and `r(modifiednum)` macros return the SIF date value for the String timestamps with corresponding names.  To display the values with date time formatting use the `%tc` formatting mask : 

``` 
. di %tc `r(accessednum)'
11dec2015 05:52:23
```

## Example 2. Make the auto.dta file executable and print the attributes to the console

```
. filesys `c(sysdir_base)'a/auto.dta, x(on) glo dis

----------------------------------------------------------------------------------------------------
    Attribute                File Attribute Value
----------------------------------------------------------------------------------------------------
    Created Date             20nov2015 05:44:54
    Modified Date            20nov2015 05:44:54
    Last Accessed Date       11dec2015 05:52:23
    Absolute File Path       /Applications/Stata/ado/base/a/auto.dta
    Canonical File Path      /Applications/Stata/ado/base/a/auto.dta
    Parent Path              /Applications/Stata/ado/base/a
    File Name                auto.dta
    Is Symbolic Link         false
    Is Regular File          true
    Is Executable            true
    Is Hidden                false
    Is Readable              true
    Is Writable              true
----------------------------------------------------------------------------------------------------

. ret li

macros:
         r(iswritable) : "true"
         r(isreadable) : "true"
         r(parentpath) : "/Applications/Stata/ado/base/a"
           r(ishidden) : "false"
           r(filename) : "auto.dta"
       r(isexecutable) : "true"
      r(canonicalpath) : "/Applications/Stata/ado/base/a/auto.dta"
        r(absoluepath) : "/Applications/Stata/ado/base/a/auto.dta"
           r(filesize) : "6443"
        r(regularfile) : "true"
            r(symlink) : "false"
        r(accessednum) : "1765432343000"
        r(modifiednum) : "1763617494000"
         r(creatednum) : "1763617494000"
           r(accessed) : "11dec2015 05:52:23"
           r(modified) : "20nov2015 05:44:54"
            r(created) : "20nov2015 05:44:54"
```

## Example 3. Remove the executable property from the auto.dta file.

```
. filesys `c(sysdir_base)'a/auto.dta, x(off) glo dis

----------------------------------------------------------------------------------------------------
    Attribute                File Attribute Value
----------------------------------------------------------------------------------------------------
    Created Date             20nov2015 05:44:54
    Modified Date            20nov2015 05:44:54
    Last Accessed Date       11dec2015 05:52:23
    Absolute File Path       /Applications/Stata/ado/base/a/auto.dta
    Canonical File Path      /Applications/Stata/ado/base/a/auto.dta
    Parent Path              /Applications/Stata/ado/base/a
    File Name                auto.dta
    Is Symbolic Link         false
    Is Regular File          true
    Is Executable            false
    Is Hidden                false
    Is Readable              true
    Is Writable              true
----------------------------------------------------------------------------------------------------

. ret li

macros:
         r(iswritable) : "true"
         r(isreadable) : "true"
         r(parentpath) : "/Applications/Stata/ado/base/a"
           r(ishidden) : "false"
           r(filename) : "auto.dta"
       r(isexecutable) : "false"
      r(canonicalpath) : "/Applications/Stata/ado/base/a/auto.dta"
        r(absoluepath) : "/Applications/Stata/ado/base/a/auto.dta"
           r(filesize) : "6443"
        r(regularfile) : "true"
            r(symlink) : "false"
        r(accessednum) : "1765432343000"
        r(modifiednum) : "1763617494000"
         r(creatednum) : "1763617494000"
           r(accessed) : "11dec2015 05:52:23"
           r(modified) : "20nov2015 05:44:54"
            r(created) : "20nov2015 05:44:54"
```
