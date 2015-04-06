# File Flags Metadata #

chflags(2) (`st_flags`) metadata support. Per-file settable attributes. Typically implemented on BSD platforms.

## Metadata supported ##

For platforms that support them:
  * User No Dump
  * User Immutable
  * User Append
  * User Opaque
  * System Archived
  * System Immutable

## Implementation status ##

Implemented since repository [revision 92](https://code.google.com/p/xar/source/detail?r=92) (2007-01-29).

## Notes ##

  * Note that some flags have overlap and may be duplicated with other metadata support. Most notably this happens with [Linux EXT2 file attributes](metadata_linux_attrib.md).
  * Archival of flags is implemented using the `st_flags` struct member of the [stat metadata](metadata_stat.md) on platforms that support it.
  * Extraction of flags is implemented using the chflags(2) APIs on platforms that support it.