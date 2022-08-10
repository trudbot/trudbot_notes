IO即input/output， 是数据在两个源之间的写入写出过程。
> 流是一种有顺序的，有起点和终点的字节集合，是对数据传输的总称或抽象。
> stream是从起源（source）到接收的（sink）的有序数据。我们这里把输入/输出源对比成“水桶”，那么流就是“管道”，这个“管道”的粗细、单向性等属性也就是区分了不同“流”的特性。


#### 字节流和字符流
IO流按操作数据的类型可以分为字符流和字节流

字节流和字符流的区别：

· 读写单位的不同：字节流以字节（8bit）为单位。字符流以字符为单位，根据码表映射字符，一次可能读多个字节。

· 处理对象不同：字节流可以处理任何类型的数据，如图片、avi等，而字符流只能处理字符类型的数据。

![](https://pic1.zhimg.com/80/v2-eb408ac849a679b09941be7ebd734768_1440w.jpg)

**javaIO流对象**
*1、输入字节流 InputStream*

从IO中输入字节流的继承图中可以看出。

1）InputStream是所有数据字节流的父类，它是一个抽象类。

2）ByteArrayInputStream、StringBufferInputStream、FileInputStream是三种基本的介质流，它们分别从Byte数组、StringBuffer、和本地文件中读取数据，PipedInputStream是从与其他线程共用的管道中读取数据。

3）ObjectInputStream和所有FileInputStream 的子类都是装饰流（装饰器模式的主角）。



*2、输出字节流 OutputStream*

从IO中输入字节流的继承图中可以看出。

1）OutputStream是所有输出字节流的父类，它是一个抽象类。

2）ByteArrayOutputStream、FIleOutputStream是两种基本的介质，它们分别向Byte 数组，和本地文件中写入数据。PipedOutputStream是从与其他线程共用的管道中写入数据。

3）ObjectOutputStream和所有FileOutputStream的子类都是装饰流。


#### 文件IO

**File类**
File类是文件（路径及文件名）的抽象， 就可以看作一个保存着文件路径的类。

File类不能用于访问文件， 但可以用于增删文件、做一些判断之类的。

File 类提供了如下三种形式构造方法。
- File(String path)：如果 path 是实际存在的路径，则该 File 对象表示的是目录；如果 path 是文件名，则该 File 对象表示的是文件。
- File(String path, String name)：path 是路径名，name 是文件名。
- File(File dir, String name)：dir 是路径对象，name 是文件名。

以下用三种方式创建了同一个文件的路径对象
```
public class Test {
    public static void main(String[] args) {
        File file1 = new File("D:\\JavaLearning\\src\\DEMO\\FileTest\\file.txt");
        File file2 = new File("D:\\JavaLearning\\src\\DEMO\\FileTest", "file.txt");

        File dir = new File("D:\\JavaLearning\\src\\DEMO\\FileTest");
        File file3 = new File(dir, "file.txt");

        System.out.println(file1 + "\n" + file2 + "\n" + file3);
    }
}
```

创建文件
```
File file1 = new File("D:\\JavaLearning\\src\\DEMO\\FileTest\\file.txt");
file1.creatNewFile()
//创建成功返回true, 文件已存在或创建失败(目录不存在)返回false
```

创建目录
```
File dir = new File("D:\\JavaLearning\\src\\DEMO\\FileTest");
dir.mkdir();
//要求路径中除最后一个目录外全要存在, 即只创建最后一个目录, 返回创建是否成功的状态

idr.mkdirs();
//创建此抽象路径名指定的目录，包括任何必需但不存在的父目录。
```
更多其它方法
方法名称|	说明
:-: | :-:
boolean canRead()|	测试应用程序是否能从指定的文件中进行读取
boolean canWrite()|	测试应用程序是否能写当前文件
boolean delete()|	删除当前对象指定的文件
boolean exists()|	测试当前 File 是否存在
String getAbsolutePath()|	返回由该对象表示的文件的绝对路径名
String getName()|	返回表示当前对象的文件名或路径名（如果是路径，则返回最后一级子路径名）
String getParent()|	返回当前 File 对象所对应目录（最后一级子目录）的父目录名
boolean isAbsolute()|	测试当前 File 对象表示的文件是否为一个绝对路径名。该方法消除了不同平台的差异，可以直接判断 file 对象是否为绝对路径。在 UNIX/Linux/BSD 等系统上，如果路径名开头是一条斜线/，则表明该 File 对象对应一个绝对路径；在 Windows 等系统上，如果路径开头是盘符，则说明它是一个绝对路径。
boolean isDirectory()|	测试当前 File 对象表示的文件是否为一个路径
boolean isFile()	|测试当前 File 对象表示的文件是否为一个“普通”文件
long lastModified()	|返回当前 File 对象表示的文件最后修改的时间
long length()|	返回当前 File 对象表示的文件长度
String[] list()|	返回当前 File 对象指定的路径文件列表
String[] list(FilenameFilter)	|返回当前 File 对象指定的目录中满足指定过滤器的文件列表
boolean mkdir()	|创建一个目录，它的路径名由当前 File 对象指定
boolean mkdirs()|	创建一个目录，它的路径名由当前 File 对象指定
boolean renameTo(File)	|将当前 File 对象指定的文件更名为给定参数 File 指定的路径名
File[] listFiles() |返回一个抽象路径名数组，表示此抽象路径名表示的目录中的文件。  

方法应用举例——遍历目录树

```java
public class Test {
    public static void main(String[] args) {
        File dir = new File("D:\\JavaLearning\\src");
        dfs(dir, 0);
    }

    public static void dfs(File file, int level)
    {
        for(int i=0; i<level; i++)
            System.out.print("  ");
        System.out.println(file.getName());
        if(file.isDirectory()) {
            File[] subFiles = file.listFiles();
            for (File subFile : subFiles) {
                dfs(subFile, level+1);
            }
        }
    }
}
/*
src
  AcWing
    性感素数
      Main.java
    校庆
      Main.java
    链表合并
      Main.java
  Algorithm
    Eratosthenes.java
    Test.java
  DEMO
    common
      AI.java
      phone.java
      Print.java
    Comparable
      Human.java
      Student.java
    Exception
      ScoreRangeException.java
      Student.java
    Figure
      circle.java
      figure.java
      FigureTest.java
      rectangle.java
    FileTest
      file.txt
      Test.java
    generic
      Generic.java
      GenericInterface.java
      impl1.java
      impl2.java
    InnerAndOuterClass
      Outer.java
    Inter
      demoInter.java
      TextClass.java
    Status
      Person.java
      Student.java
      Teacher.java
    TEST.java
  DEMO1
    Student.java
    Test.java
  MyUtil
    MyDate.java
    MyInput.java
    MyMath.java
    MyRandom.java
    MyUtil.java

*/
```
##### 文件IO字节流

**文件输出字节流**
类名：```FileOutputStream```

构造方法
```
//覆盖模式
FileOutputStream(File file)//传入文件对象
FileOutputStream(String name)//直接传入路径

//指定是否为追加模式
FileOutputStream(String name, boolean append)
FileOutputStream(File file, boolean append)
```

写入
FileOutputStream是字节流, 它对文件的写入是按字节的
```
//写入字节数组
void write(byte[] b) //将指定字节数组中的 b.length字节写入此文件输出流。 

//写入单个字节
void write(int b)// 将指定的字节写入此文件输出流。  
```
调用String类的getBytes方法可以得到字符串的字节数组表示
```
"hello".getBytes();
```
关闭输出流
```
fos.close();
```
**换行符**
windows:```\r\n```
linux:```\n```

**文件输入字节流**
类似

注意字节流能对任何格式的文件进行读取和写入

**IO字符流**
字符流是对字节流的进一步包装

**InputStreamReader**

```
InputStreamReader(InputStream in) 创建一个使用默认字符集的InputStreamReader。  
InputStreamReader(InputStream in, String charsetName) 创建一个使用指定charset的InputStreamReader。  
```
可以看到, 创建Reader对象需要传入InputStream的子类, 如FileInputStream

InputStreamReader有一个子类FileReader, 

**OutputStreamWriter**
类似

### 标准输入输出流
System有一个静态变量in, 是一个InputStream类型的对象， 可以实现读取键盘的输入

类似的还有out, err

System.out是一个PrintStream对象

**PrintStream - 字节打印流**
PrintStream是过滤输出流的儿子类， 是OutPutStream的孙子类

PrintSteam顾名思义只能写数据， 且有独有方法

```
.print(string s)//写入传入的字符串
.println(string s)//写入传入的字符串并换行

```

### 对象序列化
> 对象序列化：就是将对象保存到磁盘中，或者在网络中传输对象
这种机制就是使用一个字节序列表示个对象,该字节序列包含:对象的类型、对象的数据和对象中存储的属性等信息字节序列写到文件之后，相当于文件中持久保存了一个对象的信息
反之，该字节序列还可以从文件中读取回来，重构对象，对它进行反序列化

即写入写出对象的信息

**ObjectOutputStream**
对象序列化流

构造方法
```
//需要传入一个输出流对象
 ObjectOutputStream(OutputStream out)// 创建一个写入指定OutputStream的ObjectOutputStream。  
 ```

关键方法
```
void writeObject(Object obj) //将指定的对象写入ObjectOutputStream。
```
要注意的是被写入的对象所属类必须实现Serializable接口, Serializable接口是一个空接口, 里面没有任何方法, 仅作为标识用
```
public class Test {
    public static void main(String[] args) throws IOException {
        ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("src/DEMO/FileTest/file.txt"));
        class Student implements Serializable {
            String name, id;

            public Student(String name, String id) {
                this.name = name;
                this.id = id;
            }
        }
        Student stu = new Student("张三", "10201");
        oos.writeObject(stu);
    }
}
```
> 继承Serializable接口的属性都是基本数据类型。若是该类中有引用数据类型时，为了保证该类的实例能正常的序列化与反序列化，该类的引用数据类型对应的类也需要继承Serializable或者Extemaliazble接口。

**ObjectInputStream**
对象反序列化流, 将序列化的对象数据重新读取为一个对象

创建对象需要传入InputSteam对象, 使用关键方法readObject读取数据为对象

```
public class Test {
    public static void main(String[] args) throws IOException, ClassNotFoundException {
        class Student implements Serializable {
            String name, id;

            public Student(String name, String id) {
                this.name = name;
                this.id = id;
            }
        }

        ObjectInputStream ois = new ObjectInputStream(new FileInputStream("src/DEMO/FileTest/file.txt"));
        Student stu = (Student) ois.readObject();
        System.out.println(stu.name + " " + stu.id);
    }
}
```

**transient修饰符**
当我们希望类中的某个变量不被序列化时, 可以用transient修饰成员变量

**无效类异常**
当对象的信息被写入后又更改了类信息(即使是函数), 读取时会导致InvaildClassException


