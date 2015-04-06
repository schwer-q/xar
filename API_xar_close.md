# API Documentation #

## void xar\_close(xar\_t x) ##

Close an open xarchive handle

### Description ###

If the passed xar\_t was opened WRITE, xar\_close() will serialize the xarchive, writing the archive out to the filename specified when the xar\_t handle was opened. Then all memory associated with the xar\_t handle will be freed, and any associated file descriptors will be closed.

If the passed xar\_t was opened READ, xar\_close will free all memory associated with the xar\_t handle and close any associated file descriptors.

xar\_close() should be called whenever a xar\_t is no longer needed.

### Example ###
```
#include <xar/xar.h>

int main(int argc, char *argv[]) {
	xar_t x;

	x = xar_open(argv[1], READ);
	if( x == NULL ) {
		fprintf(stderr, "Error opening xarchive: %s\n", argv[1]);
		exit(1);
	}

	...

	xar_close(x);
	
	...

}
```