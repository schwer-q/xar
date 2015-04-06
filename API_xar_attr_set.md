# API Documentation #

## int32\_t xar\_attr\_set(xar\_file\_t f, const char **prop, const char**key, const char **value) ##
Add or set an attribute**

### Description ###
XAR attributes map to XML attributes. The XAR attribute "bar" with value "baz" on (empty) property "foo" would serialize to XML as:



&lt;foo bar="baz"/&gt;



xar\_attr\_set() can be used to add or set attributes on files or properties within a file. If the attribute does not exist, it is created. If the attribute does exist, the value is set to the value specified. No attribute may have a NULL value.

To set the attribute on a file, pass a NULL value for the second argument (the property). Here is an example of a call and what value it is modifying:
xar\_attr\_set(f, NULL, "foo", "bar");
```
<file foo="bar">
```
Similarly, to modify an attribute of a property within a file:
xar\_attr\_set(f, "name", "foo", "bar");
```
<file>
	<name foo="bar">filename</name>
</file>
```
Returns 0 for success, -1 on failure.

### Example ###
```
#include <xar/xar.h>

int main(int argc, char *argv[]) {
	xar_t x;
	xar_file_t f;

	x = xar_open(argv[1], WRITE);
	if( x == NULL ) {
		fprintf(stderr, "Error opening xarchive: %s\n", argv[1]);
		exit(1);
	}

	if( (f = xar_add(x, "/path/to/file")) == NULL ) {
		fprintf(stderr, "Error adding /path/to/file to the xarchive\n");
	}

	if( xar_attr_set(f, "name", "foo", "bar) == -1 ) {
		fprintf(stderr, "Error setting attribute\n");
	}

	...

	xar_close(x);
	
	...

}
```