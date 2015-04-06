# API Documentation #

## void xar\_iter\_free(xar\_iter\_t i) ##

Deallocates an iterator

### Description ###

xar\_iter\_free will deallocate any memory associated with the specified iterator.

### Example ###
```
#include <xar/xar.h>

int main(int argc, char *argv[]) {
	xar_t x;
	xar_file_t f;
	xar_iter_t i;

	x = xar_open(argv[1], READ);
	if( x == NULL ) {
		fprintf(stderr, "Error opening xarchive: %s\n", argv[1]);
		exit(1);
	}

	i = xar_iter_new(x);
	if( !i ) {
		fprintf(stderr, "Error obtaining a new iterator\n");
		exit(1);
	}

	f = xar_file_first(x, i);
	if( f ) {
		if( xar_extract(x, f) != 0 ) {
			fprintf(stderr, "Error adding /path/to/file to the xarchive\n");
		}
	}

	...

	xar_iter_free(i);
	xar_close(x);
	
	...

}

```