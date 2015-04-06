# API Documentation #
## xar\_subdoc\_t xar\_subdoc\_next(xar\_subdoc\_t s) ##
Get the next subdocument in an archive

### Description ###
Returns the next subdocument associated with archive. If no further subdocuments are associated with the archive, NULL is returned.

### Example ###
```
#include <xar/xar.h>

int main(int argc, char *argv[]) {
	xar_t x;
	xar_subdoc_t s;

	x = xar_open(argv[1], READ);
	if( x == NULL ) {
		fprintf(stderr, "Error opening xarchive: %s\n", argv[1]);
		exit(1);
	}

	for(s = xar_subdoc_first(x); s; s = xar_subdoc_next(s)) {
		const char *name = xar_subdoc_name(s);

		...
	}

	...

	xar_close(x);
	
	...

}
```