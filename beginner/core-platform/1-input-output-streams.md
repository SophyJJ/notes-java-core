# Input and Output With Streams and Files

- Stream = ordered sequence of data (binary or text)
- Always in pairs, one for input and one for output
- Read Abstract Classes:
  - Binary Data (Bytes)-> InputStream
  - Text Data (Chars)-> Reader
- Write Abstract Classes:
  - Binary Data (Bytes)-> OutputStream
  - Text (Chars)-> Write
- to do producer/ consumer use piped* concrete classes
- you can chain streams using their constructor
  - using try-with-resources on a higher level stream will close lower ones
  - you can also write your own high-level streams
      - extend Filter* classes (abstract) and override what you want
        - will close your enclosed stream when doing try-with-resources
- `java.io File*` are deprecated -> use `java.nio.file` instead
  - `java.nio.file` provides a lot of convenience methods to read/ write easily
  - only `java.io File*` are deprecaded. `Buffer*` and others are still in use
  - `java.nio.file` provides factories for `BufferReader`.
- a Zip file is a file system that you can create/ copy files/ read/ write to
- `Files.*`, `Paths.*`, `FileSystems.*` provide convenience methods
- If you need array with iterable, then convert it to List with `Arrays.asList(arr)`

## Error Handling (try with resources)

- need to cleanup streams. Need to make sure they close in the finally block
- you can also use try-with-resources (Java 7+)
- you can use try-with-resources (1 resource)
- ex:
```java
// read a file and output contents to screen
public static void tryWithResources() {
    char[] buff = new char[8];
    int length();
    try (Reader reader = Helper.openReader("file1.txt")) {
        while((length = reader.read(buff)) >= 0) {
            System.out.println("length " + length);
            for (int i = 0; i < length; i++) {
                System.out.print(buff[i]);
            }
        }
    }
    catch(IOException e) {
        System.out.println(e.getCalss.getSimpleName() + " - " + e.getMessage());
    }
}
```
- you can use multiple resources
- ex
```java
// read a file and write to another file
public static void tryWithResourcesMulti() {
    char[] buff = new char[8];
    int length();
    try (Reader reader = Helper.openReader("file1.txt");
         Writer writer = Helper.openWriter("file2.txt")) {
        while((length = reader.read(buff)) >= 0) {
            System.out.println("length " + length);
            Writer.write(buff, 0, length);
        }
    }
    catch(IOException e) {
        System.out.println(e.getCalss.getSimpleName() + " - " + e.getMessage());
    }
}
```
- you can write your own closeable class that you can use with try-with-resources
  - you just have to implement `AutoCloseable`
