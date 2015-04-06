# API Documentation #

## xar\_iter\_t xar\_iter\_new() ##

Allocate a new iterator

### Description ###

libxar uses iterators for browsing through the files in a xarchive, or properties associated with files. xar\_iter\_new() allocates a new iterator to be used for either of these purposes. The iterator returned must be freed when no longer needed, using xar\_iter\_free().

Upon success, xar\_iter\_new() will return a reference to a new iterator. On failure, NULL will be returned.

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

	i = xar_iter_new();
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