# API Documentation #
## xar\_subdoc\_t xar\_subdoc\_first(xar\_t x) ##
Get the first subdocument of an archive

### Description ###
Returns the first subdocument associated with archive x. If no subdocuments are associated with the archive, NULL is returned.

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