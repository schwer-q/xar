# API Documentation #

## xar\_file\_t xar\_add\_frombuffer(xar\_t x, xar\_file\_t parent, const char **name, char**buffer, size\_t length) ##

Add a file object to the archive with the data coming from an in-memory buffer.

### Description ###

xar\_add\_frombuffer() adds a single file object, represented by the in-memory buffer, to the xarchive represented by x.

The added object will be of type file.  It is important that the parent of this object be of type directory (or symliink to directory) for successful extraction.

Upon successful archival, xar\_add\_frombuffer() will return a reference to the file handle (non-zero). On failure, NULL will be returned. If an error or warning occurs while adding the file to the xarchive, the callback registered via xar\_register\_errhandler() will be invoked.

### Example ###
```
#include <xar/xar.h>

int main(int argc, char *argv[]) {
	xar_t x;
	char *buffer = "hello world";

	x = xar_open(argv[1], WRITE);
	if( x == NULL ) {
		fprintf(stderr, "Error opening xarchive: %s\n", argv[1]);
		exit(1);
	}

	if( xar_add_frombuffer(x, NULL, "myfile", buffer, strlen(buffer)) == NULL ) {
		fprintf(stderr, "Error adding /path/to/file to the xarchive\n");
	}

	...

	xar_close(x);
	
	...

}
```