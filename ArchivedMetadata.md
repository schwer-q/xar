# Explicitly archived metadata #

This is meant to be a list of metadata that xar knows about and explicitly archives.  This does not mean to be an exhaustive list of how archived information will be extracted on systems other than the one it was archived on.

  * [Generic stat information](metadata_stat.md) such as file type, permissions, uid, gid, atime, ctime, mtime.
    * Username corresponding to the uid on the system the archive was created on.
    * Group name corresponding to the gid on the system the archive was created on.
  * On systems supporting the st\_flags stat member, [the flags](metadata_chflags.md) set on the file are archived.
  * On systems supporting the [POSIX draft standard ACL](metadata_posix1e_acls.md) calls and semantics, ACLs are archived.
  * On Linux systems supporting it, on the [EXT3, JFS, Reiserfs, and XFS filesystems, Extended Attributes](metadata_linux_ea.md) are archived.
  * On [Linux system, EXT2 file attributes](metadata_linux_attrib.md) are archived (similar to but distinct from chflags() on systems supporting struct stat st\_flags)
  * On FreeBSD and NetBSD, [Extended Attributes](metadata_bsd_ea.md) are archived.
  * On Mac OS X 10.4 ACLs are archived.
  * On [Mac OS X 10.4 Extended Attributes](metadata_darwin_ea.md) (including the resource fork) is archived.
  * [Legacy Mac OS X metadata](metadata_darwin_legacy.md)
    * On Mac OS X systems, on HFS, the Finder info is archived.
    * On Mac OS X 10.3, on HFS the resource fork is archived via the ..namedfork method.
  * [Mach-O metadata](metadata_macho.md)

# Known unarchived metadata #
  * [Tru64 Extended Attributes](metadata_tru64_ea.md)
  * [Volume level metadata](metadata_volume.md)





