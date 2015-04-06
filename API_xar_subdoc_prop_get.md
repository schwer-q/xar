# API Documentation #
## int32\_t xar\_subdoc\_prop\_get(xar\_subdoc\_t s, const char **key, const char****value) ##
Get a property from a subdocument
### Description ###
If the property being retrieved, identified by key, exists in the archive, value is set to point to the value of the property and 0 is returned. If the property does not exist, -1 is returned and value is undefined. Properties can have NULL values. It is legitimate to have a successful return status, but have value be NULL. Properties can be specified in the form of "foo/bar" to create nested properties. The key "foo/bar" will retrieve the value of property "bar", which is a child of "foo". This would be similar to the XML document:
```
<foo>
	<bar>value</bar>
</foo>
```**

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
		const char *value;
		if( xar_subdoc_prop_get(s, "foo/bar", &value) == -1 ) {
			fprintf(stderr, "Property doesn't exist.\n");
			exit(2);
		}

		...
	}

	...

	xar_close(x);
	
	...

}
```