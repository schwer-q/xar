# API Documentation #
## int32\_t xar\_subdoc\_prop\_set(xar\_subdoc\_t s, const char **key, const char**value) ##
Add or set a property within a subdocument

### Description ###
If the property being set, identified by key, exists in the archive, its value is set to the specified value. If the property does not exist, it is created. Properties can be specified in the form of "foo/bar" to create nested properties. The key "foo/bar" will create a property "foo" and a child property of "foo" with the name "bar". The child property "bar" will be the property with the value specified, and "foo" will have a NULL value. This would be similar to the XML document:
```
<foo>
	<bar>value</bar>
</foo>
```

Returns 1 for success, -1 for failure.

### Example ###
```
#include <xar/xar.h>

int main(int argc, char *argv[]) {
	xar_t x;
	xar_subdoc_t s;

	x = xar_open(argv[1], WRITE);
	if( x == NULL ) {
		fprintf(stderr, "Error opening xarchive: %s\n", argv[1]);
		exit(1);
	}

	s = xar_subdoc_new(x, "subdoc");
	if( s == NULL ) {
		fprintf(stderr, "Error creating subdocument\n");
		exit(2);
	}

	if( xar_subdoc_prop_set(s, "foo/bar", "baz") == -1 ) {
		fprintf(stderr, "Error creating property foo/bar\n");
		exit(3);
	}

	...

	xar_close(x);
	
	...

}
```