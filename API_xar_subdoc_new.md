# API Documentation #

## xar\_subdoc\_t xar\_subdoc\_new(xar\_t x, const char **name) ##
Allocate and initialize a new subdocument**

### Description ###
XAR has the ability to store other XML document within its XML header, along side the archive's Table of Contents. This function allocates and initializes a structure for storing the subdocument in the archive. x is an archive to associate the subdocument with. It must have been allocated and initialized by xar\_open(). name is an identifier for the subdocument within the archive. This doesn't have to be unique, but it will make your life much easier if it is unique within the archive. On return, xar\_subdoc\_new returns a newly allocated and initialized subdocument structure, or NULL if it failed.

### Example ###
```
#include <xar/xar.h>

int main(int argc, char *argv[]) {
	xar_t x;
	xar_subdoc_t s;

	x = xar_open(argv[1], WRITE);
	if( x == NULL ) {
		fprintf(stderr, "Error opening xarchive: %s\n", argv[1]);
		exit(1);
	}

	s = xar_subdoc_new(x, "foo");
	if( s == NULL ) {
		fprintf(stderr, "Error creating new subdocument foo\n");
	}

	...

	xar_close(x);
	
	...

}
```