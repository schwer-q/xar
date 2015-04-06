# API Documentation #

## xar\_file\_t xar\_add(xar\_t x, const char **path) ##**

Add a filesystem object to a xarchive

### Description ###

xar\_add() adds a single filesystem object, represented by path, to the xarchive represented by x.

Upon successful archival, xar\_add() will return a reference to the file handle (non-zero). On failure, NULL will be returned. If an error or warning occurs while adding the file to the xarchive, the callback registered via xar\_register\_errhandler() will be invoked.

xar\_add() will treat files differently under the following circumstances:

  * The path /path/to/foo will be archived as path/to/foo, stripping out the leading /.
  * The path ../path/to/foo will be archived as path/to/foo, stripping out the leading .. The same applies to using ./path/to/foo
  * The path path/../../../to/foo will archive path non-recursively, and will archive the files at ../../to/foo as to/foo. The archive will then contain current working directory relative files/directoris of path and to.
  * In xar 1.4 and earlier, if a path of path/to/foo is given, it will treat path and path/to as directories, even if they are symlinks. However, if path is given, and path is a symlink, it will be archived as a symlink. The same is true for to if the path given is path/to. This means, if you would like either path or path/to preserved as a symlink, they must be explicitly passed to xar\_add() before calling xar\_add() with an argument of path/to/foo.
  * Post 1.4,  if a path of path/to/foo is given, path and path/to are not archived.  Instead, empty placeholder directory entires are created in the toc.  When path and path/to are later extracted, they will be created with the uid/gid of the extracting process, and permissions will be set based on umask.  No metadata for these directories is preserved.

### Behavior on different filesystem objects ###

Directory: The directory is added to the xarchive without including the directory's contents.

Regular File: The file's properties will be added to the in memory representation of the xarchive, and the file's contents will be added to the heap prior to the return of xar\_add(). If the file's link count is greater than 1, xar will look for another file in the xarchive with the same inode on the same device, and record the link information.

Symlink: The link's properties will be added to the in memory representation of the xarchive. xar\_add() will not add the file the symlink points to.

### Example ###
```
#include <xar/xar.h>

int main(int argc, char *argv[]) {
	xar_t x;

	x = xar_open(argv[1], WRITE);
	if( x == NULL ) {
		fprintf(stderr, "Error opening xarchive: %s\n", argv[1]);
		exit(1);
	}

	if( xar_add(x, "/path/to/file") == NULL ) {
		fprintf(stderr, "Error adding /path/to/file to the xarchive\n");
	}

	...

	xar_close(x);
	
	...

}
```