# Introduction #

The Python bindings for xar currently include a single Python module, [xarfile](pyxar_API_xarfile.md), which attempts to be as compatible with the Python tarfile module as reasonably possible.

pyxar is currently under active development, and as such, is incomplete. A brief "todo" list of known issues/unimplemented features is included below.

There existed a previous Python module for xar, simply named xar, but it has been deprecated.

# Download #

pyxar has been tested to work with Python 2.4 and 2.5, and has the following requirements:

  * [xar](http://code.google.com/p/xar) must be installed.
  * The Python module [pyrex](http://www.cosc.canterbury.ac.nz/greg.ewing/python/Pyrex/) must be installed.

**NOTE** Pyrex has issues with Python 2.5 and the new-style exception classes it introduced, which may cause cryptic TypeErrors when pyxar tries to raise an exception.  This should be fixed in the next Pyrex release.

You can get pyxar from xar's Subversion repository:
pyxar is currently only available from xar's Subversion repository.  It can be checked-out individually:

```
svn checkout http://xar.googlecode.com/svn/trunk/python pyxar
```

If you're checking out the entire xar repository, pyxar is located in the python subdirectory.

To build pyxar:

```
python setup.py build
```

To install pyxar:
```
python setup.py install
```

# Documentation #

pyxar's API documentation is currently available in the [xar project wiki](http://code.google.com/p/xar/w/list?q=label:pyxar). This covers the pieces of pyxar that are implemented, and should function as described. As new features are added, they will appear in this documentation.

# Issues/Todo #

  * Most errors are not properly handled
  * [XarArchive](pyxar_API_xarfile_XarArchive.md) should implement Python container methods
  * [XarArchive](pyxar_API_xarfile_XarArchive.md) needs general clean-up and organization to remove the redundant code
  * [XarInfo](pyxar_API_xarfile_XarInfo.md) filetype methods needs implementing