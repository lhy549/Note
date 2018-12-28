# IO输入输出流
## InputStream 输入流
InputStream 是一个抽象类所有输入字节流的超类。
InputStream提供了一种返回输入的下一个字节的方法。

使用了方法重载：

    //从输入流读取数据的下一个字节。值字节被返回作为int范围0至255 。 
    //如果没有字节可用，因为已经到达流的末尾，则返回值-1 。
    //该方法阻塞直到输入数据可用，检测到流的结尾，或抛出异常。 
    public abstract int read() throws IOException;
    
    //从输入流读取一些字节数，并将它们存储到缓冲区b
    public abstract int read(byte[] b) throws IOException;
    public abstract int read() throws IOException;








它的子类：

### AudioInputStream
### ByteArrayInputStream
### FileInputStream
### FilterInputStream
### ObjectInputStream
### PipedInputStream
### SequenceInputStream
### StringBufferInputStream



### 






## OutputStream 输出流