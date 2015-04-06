# API Documentation #

## const char **xar\_attr\_get(xar\_file\_t f, const char**prop, const char **key) ##
Add or set an attribute**

### Description ###
XAR attributes map to XML attributes. The XAR attribute "bar" with value "baz" on (empty) property "foo" would serialize to XML as:
```
<foo bar="baz"/>
```
xar\_attr\_get() can be used to get attributes on files or properties within a file.

To get the attribute on a file, pass a NULL value for the second argument (the property). Here is an example of a call and what value it is retrieving:
const char **value = xar\_attr\_get(f, NULL, "foo");
printf("Attribute foo of the file is: %s\n", value);**

Attribute foo of the file is: bar
```
<file foo="bar">
```
Similarly, to modify an attribute of a property within a file:
const char **value = xar\_attr\_get(f, "name", "foo");
printf("Attribute "foo" of property "name" of the file is: %s\n", value);**

Attribute "foo" of property "name" of the file is: bar
```
<file>
	<name foo="bar">filename</name>
</file>
```
Returns a pointer to the value of the attribute, if it exists. NULL is returned if the attribute does not exist. No attribute may have a NULL value.

### Example ###
```
#include <xar/xar.h>

int main(int argc, char *argv[]) {
	xar_t x;
	xar_file_t f;
	const char *value;

	x = xar_open(argv[1], WRITE);
	if( x == NULL ) {
		fprintf(stderr, "Error opening xarchive: %s\n", argv[1]);
		exit(1);
	}

	if( (f = xar_add(x, "/path/to/file")) == NULL ) {
		fprintf(stderr, "Error adding /path/to/file to the xarchive\n");
		exit(2);
	}

	value = xar_attr_get(f, NULL, "id");
	if( value == NULL ) {
		fprintf(stderr, "Error getting the id of the file\n");
		exit(3);
	}

	printf("/path/to/file's id is: %s\n", value);

	...

	xar_close(x);
	
	...

}
```