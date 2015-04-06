# API Documentation #

## xar\_file\_t xar\_file\_next(xar\_iter\_t i) ##

Obtain a reference to the next file in a xarchive

### Description ###

libxar uses iterators for browsing through the files in a xarchive, or propertie s associated with files. xar\_file\_next() takes an iterator previously allocated with a call to xar\_iter\_new() and initialized with a call to xar\_file\_first(). xar\_file\_next() will then return a reference to the next file in the xarchive. This function is meant to allow linear iteration over the files in a xarchive.

Upon success, xar\_file\_next() will return a reference to the next file in the xarchive. On failure, NULL will be returned.

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

	for(f = xar_file_first(x, i); f; f = xar_file_next(i)) {
		xar_extract(x, f);
	}

	...

	xar_iter_free(i);
	xar_close(x);
	
	...

}

```