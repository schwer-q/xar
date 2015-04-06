# API Documentation #
## const char **xar\_subdoc\_name(xar\_subdoc\_t s) ##
Get the name of a subdocument
### Description ###
Retrieves the name of the specified subdocument and returns a pointer to it.**

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