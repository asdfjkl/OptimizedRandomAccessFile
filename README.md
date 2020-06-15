# OptimizedRandomAccessFile

Java's `RandomAccessFile` is slow, as there is no buffering. However it allows both random access to data and line-by-line reading via `readLine()`, and thus is quite handy if you want to operate on large files (binary or text). 

This is a drop-in replacement for Java's RandomAccessFile that adds buffering, originally available @ https://bitbucket.org/kienerj/io/src/default/ 

The original version treated all characters as chars; this updated version allows to handle any kind of text encoding. Consider for example 

       try {
       OptimizedRandomAccessFile raf = new OptimizedRandomAccessFile(filename, "r");
       String line = raf.readLine();
       String utf8 = new String(line.getBytes("ISO-8859-1"), "UTF-8");
       System.out.println(utf8);
       } catch (IOException e) {
       e.printStackTrace();
       }

The version available on maven is outdated and does not contain the update.

All credits to the original author Joos Kiener. The original readme is below.

# IO

Classe(s) for improving IO in Java. Currently there is only 1 class in this library.
OptimizedRandomAccessFile

`java.io.RandomAccessFile` has a `readLine()` method with terrible performance. It reads files byte per byte and that is very slow.

`OptimizedRandomAccessFile` wraps `java.io.RandomAccessFile` and exposes all methods while having a `readLine()` method that performs similar to `java.io.BufferedReader` and hence about 100 times faster than that of `java.io.RandomAccessFile` while preserving correct random access.
