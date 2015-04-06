# "POSIX" stat Metadata #

"POSIX"-ish [stat](http://www.opengroup.org/onlinepubs/009695399/functions/stat.html) metadata.

## Metadata supported ##

  * Type of file (file, hardlink, link)
    * Broken links
  * File mode (UNIX-like permissions)
  * UID
    * Textual user representation of UID on archiving system
  * GID
    * Textual group representation of GID on archiving system
  * atime, ctime, and mtime (in [ISO 8601](http://en.wikipedia.org/wiki/ISO_8601) format)

## Implementation status ##

Implemented since >= 1.0

## Notes ##

  * On systems that support the `st_flags` member of the `stat` struct xar will archive the [chflags(2)](metadata_chflags.md) flags.