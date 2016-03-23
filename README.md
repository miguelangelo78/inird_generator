# initrd Generator
This simple C program creates a very basic filesystem (extremely basic) in order to load it easily on a Hobby OS


----------

Building
--------
Simply build with the command:
`> make -f makefile.mak`

Running
--------
In order to make an initrd file, simply run:
```> initrd_gen file1 file2 file3 [...]```

What filesystem is it creating?
--------
The struct that defines the filesystem is as follows:
```
struct {
	unsigned int header_size; /* 4 Bytes */
	unsigned int file_count; /* 4 Bytes */
	unsigned int * offset, * length; /* 4 Bytes each entry. Each entry indicates the start of each file, and the length as well */
	char ** filename; /* Might be 4 bytes as a pointer, but on the disk it'll be 1 byte per character */
} initrd_header;
```

![initrd filesystem diagram](http://i.imgur.com/uRsDq2v.png)

**VERY IMPORTANT NOTE**: There is a missing field on the diagram. Right after the 'File Lengths' field, the Filenames' field starts. The field is exactly the same as the Offsets and Lengths' field, except each filename is terminated with a null character (for obvious reasons).
