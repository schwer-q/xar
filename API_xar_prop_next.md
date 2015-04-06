# API Documentation #

## const char **xar\_prop\_next(xar\_iter\_t i) ##
Obtain a reference to the next property in a xarchive**

### Description ###
libxar uses iterators for browsing through the files in a xarchive, or properties associated with files. xar\_prop\_next() takes an iterator previously allocated with a call to xar\_iter\_new() and initialized with a call to xar\_prop\_first(). xar\_prop\_next() will then return a reference to the next property key associated with the file the xar\_iter\_t was initialized with. The function is meant to allow linear iteration over the files in a xarchive.

Upon success, xar\_prop\_next() will return a reference to the next property key in the file.

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

	for( f = xar_file_first(x, i); f; f = xar_file_next(i) ) {
		const char *key;
		xar_iter_t p;
	
		p = xar_iter_new(x);
		for( key = xar_prop_first(f, p); key; key = xar_prop_next(p) ) {
			const char *val = NULL; 
			xar_prop_get(f, key, &val);
			printf("key: %s, value: %s\n", key, val);
		}
		xar_iter_free(p);
	}

	...

	xar_iter_free(i);
	xar_close(x);
	
	...

}
```