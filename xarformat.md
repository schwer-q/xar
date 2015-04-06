# Format of a xar archive #

The XAR file format has three main regions, The Header, The Table of Contents, and The Heap. The header is a small binary data structure that identifies the file format (file magic). The table of contents is parsed as an XML document. The heap occupies the remainder of the file. Files' data are stored in the heap.

## The Header ##

The header starts with 32 bits of file magic ('xar!') in network byte order. The next 16 bits are the size of the header (including the 32 bits of file magic) in network byte order. A 16 bit xar file version number follows in network byte order, the current version is zero. Last is the 64 bit length of the table of contents regions, also in network byte order. The header may be represented as the following xar\_header C structure.

```
#define XAR_HEADER_MAGIC 0x78617221
#define XAR_HEADER_VERSION 0
#define XAR_HEADER_SIZE sizeof(struct xar_header)

/*
 * xar_header version 0
 */
struct xar_header {
    uint32_t magic;	
    uint16_t size;
    uint16_t version;
    uint64_t toc_length_compressed;
    uint64_t toc_length_uncompressed;
    uint32_t cksum_alg;
};
```

## The Table of Contents ##

The table of contents is an XML document. The table of contents should be encoded as UTF-8.

```
<?xml version="1.0"?>

<xar>
  <toc>
    <checksum style="sha1">
      <size>20</size>
      <offset>0</offset>
    </checksum>
    <file id="1">
      <name>xar</name>
      <type>file</type>
      <mode>0755</mode>
      <uid>0</uid>
      <gid>0</gid>
      <user>root</user>
      <group>wheel</group>
      <size>81180</size>
      <data>
        <offset>0</offset>
        <size>74108</size>
        <length>23083</length>
        <extracted-checksum style="md5">d852c77ac3c8e83f312c12b4c3198e6d</checksum>
        <archived-checksum style="md5">ceaf793ccb1990ecbadb20112d5f9e5d</checksum>
        <encoding style="application/x-gzip"/>
      </data>
      <ea>
        <name>com.apple.ResourceFork</name>
        <offset>0</offset>
        <size>7072</size>
        <length>3942</length>
        <extracted-checksum style="md5">0f7061dca2d7411352377db0e53792db</checksum>
        <archived-checksum style="md5">c72de8ac25abe462a930254d82958534</checksum>
        <encoding style="application/x-gzip"/>
      </ea>
    </file>
  </toc>
</xar>
```

## The Heap ##

As its name suggests, the heap is an unstructured heap of data referenced by the table of contents. It is recommended that implementations use the heap as efficiently as possible and defragment the heap during archive creation as well order it sensibly. In order for an archive to be streamable, it is necissary for all of a file's heap entries to be grouped together, with extended attributes coming before the data portion of the file. When streaming, the heap entries will be extracted in the order they appear, and the EA data must be extracted before the data so the proper security context can be set on the file before the data is extracted.