# API Documentation #

## int32\_t xar\_prop\_set(xar\_t x, const char **key, const char**value) ##

Add/set a property

### Description ###

XAR properties are the equivalent of XML tags. For example, a XAR property of "foo" with a value of "bar" would serialize in XML to become:
```
<foo>
	<bar>
</foo>
```

xar\_prop\_set() will create a new property if it doesn't already exist, and if the property does exist, its value is set to the value specified. Properties can be specified using '/'s as parent/child delimiters. For example, using "foo/bar" will map to the XML equivalent of:
```
<foo>
	<bar>value</bar>
</foo>
```

Properties may have NULL values. The return value is 0 for success, -1 for failure.

The normal keys for files and their values are:
|name |	The name of the file. If the filename is not representable in UTF8, the filename is base64 encoded and an "encoding" attribute specifies that the name is in base64 encoding.|
|:----|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|type |file, directory, fifo, character special, block special, socket |
| uid |	a numeric string representing the file's unix user id |
| gid |	a numeric string representing the file's unix user id |
| mode |	Octal numeric string representing the file's unix permissions |
| user |	The username mapping for the user owning the file at the time and on the system it was archived. |
| group |	The group name mapping for the user owning the file at the time and on the system it was archived. |
| size |	a numeric string representing the overall size of the file|

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

	f = xar_add(x, "/tmp/foo");
	if( f == NULL ) {
		fprintf(stderr, "Error adding file to the archive\n");
		exit(2);
	}

	xar_prop_set(f, "foo", "bar");

	...

	xar_close(x);
	
	...

}

```




