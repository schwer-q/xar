The XAR project aims to provide an easily extensible archive format. Important design decisions include an easily extensible XML table of contents for random access to archived files, storing the toc at the beginning of the archive to allow for efficient handling of streamed archives, the ability to handle files of arbitrarily large sizes, the ability to choose independent encodings for individual files in the archive, the ability to store checksums for individual files in both compressed and uncompressed form, and the ability to query the table of content's rich meta-data.

Documentation:
  * [API](API_xar.md)
  * [file format](xarformat.md)
  * [pyxar](pyxar.md) python bindings
  * [Metadata](ArchivedMetadata.md) archived by XAR (living document)
  * [Why](whyxar.md) XAR is interesting

XAR in use:
  * [Mac OS X 10.5](http://www.apple.com/macosx/) Installer uses xarchives
  * [RPM5](http://rpm5.org) The new rpm format uses xar
  * [Compress Files](http://www.apimac.com/compress_files/) for Mac OS X
  * [Endeavour Mark II](http://www.battlefieldlinux.com/wolfpack/Endeavour2/) Unix File Management Suite
  * [SArchiveKit](http://code.google.com/p/sarchivekit/) an Obj-C wrapper for libxar