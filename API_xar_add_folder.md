# API Documentation #

## xar\_file\_t xar\_add\_folder(xar\_t x, xar\_file\_t f, const char **name, struct stat**info) ##

Add a directory object to a xarchive

### Description ###

xar\_add\_folder() adds a single directory object, represented by the passed file name and struct stat, to the xarchive represented by x.

Upon successful archival, xar\_add\_folder() will return a reference to the file handle (non-zero). On failure, NULL will be returned. If an error or warning occurs while adding the file to the xarchive, the callback registered via xar\_register\_errhandler() will be invoked.

### Example ###
```
#include <xar/xar.h>

int main(int argc, char *argv[]) {
	xar_t x;
	struct stat sb;

	x = xar_open(argv[1], WRITE);
	if( x == NULL ) {
		fprintf(stderr, "Error opening xarchive: %s\n", argv[1]);
		exit(1);
	}

	memset(&sb, 0, sizeof(sb));
	sb.st_mode = S_IFDIR | S_IRWXU;

	if( xar_add(x, NULL, "mydir", &sb) == NULL ) {
		fprintf(stderr, "Error adding mydir to the xarchive\n");
	}

	...

	xar_close(x);
	
	...

}
```