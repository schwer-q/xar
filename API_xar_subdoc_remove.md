# API Documentation #
## void xar\_subdoc\_remove(xar\_subdoc\_t s) ##
Removes and deallocates a subdocument from a xarchive

### Description ###
xar\_subdoc\_remove() removes and frees a subdocument from a XAR archive. The entire subdocument is removed, all children, properties, attributes, etc. associated with the subdocument are removed.

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

	s = xar_subdoc_first(x);
	if( s )
		xar_subdoc_remove(s);

	...

	xar_close(x);
	
	...

}
```