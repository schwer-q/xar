# API Documentation #
## int32\_t xar\_subdoc\_copyout(xar\_subdoc\_t s, unsigned char buf, unsigned int **size) ##
Serialize a xar\_subdoc\_t to an in-memory buffer**

### Description ###
Serializes a subdocument to an in memory buffer. xar\_subdoc\_copyout() allocates memory for a buffer, serializes the document into it, then set buf to point to the allocated buffer, and size to the length of the buffer. The caller is responsible for calling free() on buf. On success, 0 is returned. -1 on failure. If the call fails, buf and size have undefined values.

### Example ###
```
#include <xar/xar.h>

int main(int argc, char *argv[]) {
	xar_t x;

	x = xar_open(argv[1], READ);
	if( x == NULL ) {
		fprintf(stderr, "Error opening xarchive: %s\n", argv[1]);
		exit(1);
	}

	for(s = xar_subdoc_first(x); s; s = xar_subdoc_next(s)) {
		unsigned char *buf;
		unsigned int size;

		xar_subdoc_copyout(s, &buf, &size);
		printf("%s\n", buf);
		free(buf);

		...
	}

	...

	xar_close(x);
	
	...

}
```