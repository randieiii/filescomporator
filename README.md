# files finder
Script to find all similar files in a certain directory and replace them with hardlinks.

# Use:

```
  python3 ./check.py <your directory>
```

# Test:

Example of directory:

```
tree .
.
├── f
│   ├── k
│   │   ├── test4.txt
│   │   └── test5.txt
│   └── test3.txt
├── __pycache__
│   └── fuse.cpython-36.pyc
├── test2.txt
└── test.txt
```
Checking if there are hardlinks in directory:

Before script:
```

stat test.txt 
  File: test.txt
  Size: 83        	Blocks: 8          IO Block: 4096   regular file
Device: 805h/2053d	Inode: 262242      Links: 1 # <<-- only one link


find -samefile ./test.txt 
./test.txt <-finds the only one file

```
After script:

```
stat test.txt 
  File: test.txt
  Size: 83        	Blocks: 8          IO Block: 4096   regular file
Device: 805h/2053d	Inode: 28376       Links: 5 # <<-- a lot of links

find -samefile ./test.txt 
./test.txt
./f/test3.txt
./f/k/test5.txt
./f/k/test4.txt
./test2.txt << -- a lot of files
```
