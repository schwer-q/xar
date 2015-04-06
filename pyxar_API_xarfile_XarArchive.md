# pyxar API Documentation #

## XarArchive(...) ##

This class provides an interface to a xar archive file.  Each archive member is represented by a XarInfo object.

The XarArchive class provides methods for accessing members and subdocs, and additionally provides a standard Python container API.

All archive members are represented by [XarInfo](pyxar_API_xarfile_XarInfo.md) objects, and a [XarInfo](pyxar_API_xarfile_XarInfo.md) object will be returned by any method that returns a member unless otherwise stated.

### Accessing Members ###

> #### getmembers(...) ####
> > Return the members as a list of  objects.


> #### getmember(...) ####
> > Return a XarInfo object for the member


> #### getnames(...) ####
> > Return the members as a list of their names.


> #### items(...) ####
> > Return a list of tuples of (name, member) for the members in the archive.


> #### get(...) ####
> > Return the member for the given name, or the given default if the name doesn't exist


> #### has\_key(...) ####
> > Return whether the archive contains the given name


> #### iteritems(...) ####

> #### iterkeys(...) ####

> #### itervalues(...) ####

> #### keys(...) ####

> #### values(...) ####

### Accessing Subdocs ###

> #### getsubdoc(...) ####
> > Return a XarSubdoc object for the subdoc of the given name


> #### getsubdocnames(...) ####
> > Return a list of the names of each subdoc in the archive.


> #### getsubdocs(...) ####
> > Return a list of XarSubdoc objects for each subdoc in the archive.

### Mutation ###


> #### add(...) ####
> > Add a file (or directory) to the archive, if the archive is writable.  If the name is a directory, and recursive is True, then add the directory recursively.


> #### extract(...) ####
> > Extract the member to the given path, or the current directory if no path is given. If no member is given, every file in the archive is extracted to the given path, or the current directory.


> #### addsubdoc(...) ####
> > Adds the given subdoc to the xar archive.  Subdoc is assumed to be an instance of [XarSubdoc](pyxar_API_xarfile_XarSubdoc.md), but if not, it is assumed to be a path to an xml file that can be used to create a [XarSubdoc](pyxar_API_xarfile_XarSubdoc.md) instance.


> #### removesubdoc(...) ####
> > Remove the subdoc of the given name from the archive.

### Miscellaneous ###


> #### getxarinfo(...) ####
> > Create a XarInfo object for the given file name that is NOT in the [XarArchive](pyxar_API_xarfile_XarArchive.md).


> #### open() ####
> > Open the [pyxar\_API\_xarfile_XarArchive XarArchive]_


> #### close() ####
> > Close the [pyxar\_API\_xarfile_XarArchive XarArchive].  This method is called implicitly upon deallocation, if not explicitly prior._





