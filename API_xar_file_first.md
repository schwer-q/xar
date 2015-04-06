# API Documentation #

## xar\_file\_t xar\_file\_first(xar\_t x, xar\_iter\_t i) ##

Obtain a reference to the first file in a xarchive

### Description ###

libxar uses iterators for browsing through the files in a xarchive, or propertie s associated with files. xar\_file\_first() takes a xar\_t as returned by a call to xar\_open() and an iterator previously allocated with a call to xar\_iter\_new(). xar\_file\_first() will then return a reference to the first file associated with the xarchive represented by the passed xar\_t.

Upon success, xar\_file\_first() will return a reference to the first file in the xarchive. On failure, NULL will be returned.

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