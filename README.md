# FILESYS

A Stata program to access and modify file system properties.  Currently, the program/plugin allow users to:

1. Access file attributes 
2. Set the file to be executable globally or for the owner only
3. Set the file to be readable globally or for the owner only
4. Set the file to be writable globally or for the owner only
5. Make a file readonly protected

## Requirements
Plugin is compiled under Java 8.  Should not be a problem for most installations of Stata, but if you have an older JVM you can alter the JVM used by setting the appropriate properties.  To see the java property names use `query java`.


