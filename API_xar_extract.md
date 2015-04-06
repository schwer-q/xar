# API Documentation #

## int32\_t xar\_extract(xar\_t x, xar\_file\_t f) ##

Extract a file from a xarchive

### Description ###

xar\_extract() will extract a single filesystem object from the specified xarchive. Only the object specified by f will be extracted. xar\_extract() will not recurse and extract children of f. The file will be extracted relative to the current working directory, with the path and filename of the file in the archive. For example, if a file was archived with a path of "/path/to/file", the file will be extracted relative to the current working directory as "path/to/file".

Upon success, xar\_extract() will return 0. On failure, -1 will be returned. If any errors or warnings occur during extraction, the callback registered via xar\_register\_errhandler will be invoked.

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
			fprintf(stderr, "Error extracting /path/to/file from the xarchive\n");
		}
	}

	...

	xar_iter_free(i);
	xar_close(x);
	
	...

}

```