# API Documentation #

## const char **xar\_attr\_next(xar\_iter\_t i) ##
Obtain a reference to the next attribute associated with the property in the file associated with the xar\_iter\_t**

### Description ###
libxar uses iterators for browsing through the files in a xarchive, or properties associated with files, and attributes associated with properties. xar\_attr\_next() takes an iterator previously allocated with a call to xar\_iter\_new() and initialized with a call to xar\_attr\_first(). xar\_attr\_next() will then return a reference to the next attribute key associated with the property and file associated with the xar\_iter\_t. This function is meant to allow linear iteration over the attributes of a property.

Upon success, xar\_attr\_next() will return a reference to the next attribute key associated with the specified property in the specified file.

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
			xar_iter_t a;
			const char *akey;

			a = xar_iter_new(x);
			for( akey = xar_attr_first(f, key, a); akey; akey = xar_attr_next(a) ) {
				const char *aval = NULL;

				akey = xar_attr_get(f, key, akey);
				printf("prop: %s, attribute key: %s, attribute value: %s\n", key, akey, aval);
			}
			xar_iter_free(a);
		}
		xar_iter_free(p);
	}

	...

	xar_iter_free(i);
	xar_close(x);
	
	...

}
```