# compression-challenge

I have provided five binary files in a secret format. These files are each several megabytes, summing to ~30MB.

```bash
$ du -k files/*
6000    files/file1
2932    files/file2
6000    files/file3
4208    files/file4
2836    files/file5
4504    files/file6
4884    files/file7
$ du -k files/
31368   files/
```

Your goal is to create a compression and decompression algorithm that achieves at least a ~9x reduction in size, including the size of the compression and decompression program.

```bash
$ mkdir compressed
$ for i in {1..7}; do ./solution compress -input files/file${i} -output compressed/file${i}; done
$ du -k compressed/*
32      compressed/file1
4       compressed/file2
32      compressed/file3
156     compressed/file4
16      compressed/file5
212     compressed/file6
232     compressed/file7
$ du -k compressed/
688     compressed/
$ du -k solution 
2304    solution
```

Here, the compressed data is now 0.7MB, and the compression program itself is 2.3MB. This totals to 2.99MB, which is less than 10x the size of our original data (~31MB).

The compression is required to be lossless. This means that we can now decompress this data into the original files, and they must be bit-for-bit equal.

```bash
$ mkdir decompressed
$ for i in {1..7}; do ./solution decompress -input compressed/file${i} -output decompressed/file${i}; done
$ sum decompressed/*
60340  5997 decompressed/file1
49613  2930 decompressed/file2
14037  5997 decompressed/file3
37567  4205 decompressed/file4
01491  2833 decompressed/file5
00669  4503 decompressed/file6
06482  4884 decompressed/file7
$ sum files/*
60340  5997 files/file1
49613  2930 files/file2
14037  5997 files/file3
37567  4205 files/file4
01491  2833 files/file5
00669  4503 files/file6
06482  4884 files/file7
```

# Rules

 * You must include the size of your compressor + decompressor when computing the compression ratio.
 * You may not store secret information in filenames or other metadata that is not counted in the compressed size.
 * Your compression algorithm must be lossless; the decompressed data must match the original data before compression, byte-for-byte.
 * You may not find your solution by hacking my computer or my online accounts!
