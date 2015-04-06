# API Documentation #
## int32\_t xar\_subdoc\_copyin(xar\_subdoc\_t s, unsigned char **buf, unsigned int size) ##
Unserialize an in-memory buffer to a xar\_subdoc\_t**

### Description ###
Unserializes an xml document contained in memory pointed to by buf. The subdocument structure, s, should have been allocated and initialized by a call to xar\_subdoc\_new(). On return, the subdocument s is populated from the xml document pointed to by buf (the length of buf described by the size parameter). On success, 0 is returned. On failure, -1 is returned.

### Example ###
```
#include <xar/xar.h>

int main(int argc, char *argv[]) {
	xar_t x;
	xar_subdoc_t s;
	unsigned char *foo = "<foo><bar>baz</bar></foo>";
	unsigned int len = strlen(foo);

	x = xar_open(argv[1], WRITE);
	if( x == NULL ) {
		fprintf(stderr, "Error opening xarchive: %s\n", argv[1]);
		exit(1);
	}

	s = xar_subdoc_new(x);
	if( !s ) {
		fprintf(stderr, "Error creating new subdocument\n");
		exit(2);
	}

	if( xar_subdoc_copyin(s, buf, len) == -1  ) {
		fprinntf(stderr, "Error unserializing subdocument\n");
		exit(3);
	}

	...

	xar_close(x);
	
	...

}
```