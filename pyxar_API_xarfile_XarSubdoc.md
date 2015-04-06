# pyxar API Documentation #

## XarSubdoc(...) ##

This class represents a xar subdoc that is stored in the archive. It provides access to the XML, ability to extract to a file, and a convenience parser method.

> ### XarSubdoc(name, xml) ###
> > Creates a [XarSubdoc](pyxar_API_xarfile_XarSubdoc.md) instance with the given name containing the given XML string. Instance creation is only useful when adding a subdoc to a xar archive.


> ### toxml() ###
> > Returns the subdoc as an XML string.


> ### tofile(...) ###
> > Write the XML string to a file by the given filename.


> ### parse(...) ###
> > Parse the document's xml string using the given function. This assumes the function takes a single string argument.