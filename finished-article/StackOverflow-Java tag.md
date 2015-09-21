#关于 [java](!http://stackoverflow.com/questions/tagged/java)

Java (请不要与 JavaScript 搞混) 是一种设计为与 Java 虚拟机 （JVM） 一起使用的多用途编程语言。一般称呼安装了相关工具使其可以开发并运行 Java 程序的电脑系统为 “Java 运行平台”。使用这个标签可以查找有关 Java 编程语言或者 Java 平台工具的问题。

[Java](http://www.java.com/en/) 是一种高性能、跨平台、[面向对象](http://en.wikipedia.org/wiki/Object-oriented_programming)的编程语言和运行环境。Java 大部分语法起源于 [C](http://stackoverflow.com/questions/tagged/c) 和 [C++](http://stackoverflow.com/questions/tagged/c%2b%2b)，但是其对象模型简于 [C++](http://stackoverflow.com/questions/tagged/c%2b%2b)，并且减少了低级功能。Java 应用均被编译为**字节码**（被称为 **class** 文件），使其可以被 [JVM](http://stackoverflow.com/questions/tagged/jvm)（Java 虚拟机）执行，并独立于不同的电脑体系。[JVM](http://stackoverflow.com/questions/tagged/jvm) 通过一个**垃圾收集器**（查看 [garbage-collection](http://stackoverflow.com/questions/tagged/garbage-collection)）帮助管理内存，当对象不再使用时可以将其从内存中移除。Java 的[系统类型](http://en.wikipedia.org/wiki/Type_system)是静态、强类型、安全、声明类型和显式的。Java 支持反射、接口等与 [C](http://stackoverflow.com/questions/tagged/c) 和 [C++](http://stackoverflow.com/questions/tagged/c%2b%2b) 相似的功能，例如 [JNI](http://stackoverflow.com/questions/tagged/jni)（The Java Native Interface）。

[Java](!http://stackoverflow.com/questions/tagged/java) 被设计为尽可能减少与电脑系统的依赖关系，可以允许应用开发者 “一处编写，处处运行”（[WORA](http://en.wikipedia.org/wiki/Write_once,_run_anywhere)）：在一个平台上执行的代码不需重新编译就能在其他机器上运行。Java 最初由 [James Gosling](http://en.wikipedia.org/wiki/James_Gosling) 在 Sun Mircosystems 公司（2009年4月20日已被 Oracle 并购）设计，最初是于 1995 年作为 Sun Microsystems公司 Java 运行平台的核心元件发行。

安装工具用于开发和运行 Java 的电脑系统被 Sun（现为 Oracle）命名为 [Java 运行平台](http://en.wikibooks.org/wiki/Java_Programming/The_Java_Platform)。各种具有平台特性的工具可以帮助开发者更有效率地使用  Java 程序语言开发。

平台包含两个基本的软件包：

 - **Java 运行环境（JRE）**：用于运行 Java 应用和程序；
 - **Java 开发工具包（JDK）**：用于开发 Java 应用和程序。JDK 总是伴随着一个 JRE。

在本节中，我们将进一步探讨这两个软件包作为 Java 运行平台的组成部分，其产生的作用。

##背景

作为参考的大部分 Java 实现方式都是开源的（the [OpenJDK](http://openjdk.java.net/)），由包括 Oracle，Apple，SAP 与 IBM 在内的大型企业提供支持。

极少的电脑可以直接运行 Java 程序。因此，Java 环境通常要求安装合适的软件组件。在 Windows 系统上，一般可以从 [java.com](http://www.java.com/en/) 下载免费的 Java 运行环境（JRE）。在 Macintosh 系统上，当一个应用需要 Java 运行环境时，会在启动时请求用户下载 Java。在类  [Linux](http://stackoverflow.com/questions/tagged/linux) 系统上，Java 一般通过包管理器安装。

Windows 和 Mac 平台的开发者经常需要额外的工具，使用工具所需的免费 Java 开发包（JDK）必须从 [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html)下载并手动安装。

Java 会被编译为字节码，然后由 JVM 通过编译为原生代码进行解析工作。编译技术为[动态编译](http://en.wikipedia.org/wiki/Just-in-time_compilation)（JIT）。最初这被视为降低性能的做法，但是随着 JVM 和 JIT 的发展，担忧逐渐减少。在某些情况下，例如当一个旧版本的处理器需要向后兼容时，JVM 甚至快于原生代码编译速度。

注意：也有其他供应商存在，然而大部分都有授权费。对于 [linux](http://stackoverflow.com/questions/tagged/linux) 和其他平台，请查阅相关的操作系统文档。

##版本

包含主要的 Java 版本，代号和发行时间：
 
 - JDK 1.0                  (1996/01/23)
 - JDK 1.1                  (1997/02/19)
 - J2SE 1.2    [Playground] (1998/12/08)
 - J2SE 1.3    [Kestrel]    (2000/05/08)
 - J2SE 1.4    [Merlin]     (2002/02/06)
 - J2SE 5.0    [Tiger]      (2004/09/30)
 - Java SE 6   [Mustang]    (2006/12/11)
 - Java SE 7   [Dolphin]    (2011/07/28)
 - Java SE 8   [JSR 337]    (2014/03/18)
 - Java SE 9   [TBD    ]    (未发布)

最新的稳定版本：

 - Java Standard Edition 8 Update 51 (1.8.0_51) - (2015/07/14)
 - Java Standard Edition 7 Update 79 (1.7.0_79) - (2015/04/14)

更多的代号及发行日期请访问 [J2SE Code Names](http://www.oracle.com/technetwork/java/javase/codenames-136090.html)。要查看 JDK 的版本发行日志请访问 [Wikipedia](http://en.wikipedia.org/wiki/Java_version_history) 的 Java 版本历史文章。

Java SE 8 正在发行并且可[下载](http://www.oracle.com/technetwork/java/javase/downloads/index.html)。

[公共更新](http://www.oracle.com/technetwork/java/eol-135779.html)的结束日期（以前称为结束生命）为：

 - J2SE 1.4   -  2008/10
 - J2SE 5.0   -  2009/10
 - Java SE 6  -  2013/02
 - Java SE 7  -  2015/04
 - Java SE 8  -  2017/09

##初始帮助

你是 Java 初学者或者需要帮助使你的第一个 Java 程序运行？请参看 [Oracle Java 教程开始部分](http://docs.oracle.com/javase/tutorial/getStarted/index.html)。

询问问题前，请使用右上角的搜索栏查找是否已被询问（我们有很多相似的问题），并且阅读[《如何提出一个好的问题》](http://blogs.msmvps.com/jonskeet/2010/08/29/writing-the-perfect-question/)，学习怎样吸引 Jon Skeet 回答你的问题。

##命名规范

Java 程序需要坚持下列的[命名规范](http://docs.oracle.com/javase/specs/jls/se8/html/jls-6.html)以提高可读性和降低意外错误出现的可能性。通过遵守这些命名规范，可以使他人阅读你的代码和帮助你时更加轻松。

**类型名**（类，接口，枚举等等）应以大写字母开头，随后的每个单词首字母大写。例如：```String```，```ThreadLocal``` 和 ```NullPointerException```。有时被称为 pascal case（帕斯卡命名法）。

**方法名**应使用 camelCased（驼峰式命名法），即它们应以小写字母开头，随后的每个单词首字母大写。例如：indexOf，printStackTrace，interrupt。

**字段名**应使用和方法名一样的驼峰式命名法。

**常量表达式命名**（```static final``` 不可变对象）应被写为 ALL_CAPS形式，使用下划线分割每个单词。例如：```YELLOW```，```DO_NOTHING_ON_CLOSE```。这同样应用于一个枚举类（```Enum```）的变量命名。然而，```static final``` 修饰可变对象时应使用驼峰式命名。

##Hello World - 你的第一个程序

**Hello World** 程序的代码为：

``` java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

编译和调用 **Hello world** 程序：

``` shell
javac -d . HelloWorld.java 
java -cp . HelloWorld
```

Java 源代码被编译为中间代码形式（针对 [Java 虚拟机](http://en.wikipedia.org/wiki/Java_virtual_machine) 的字节码指令），然后可以被 ```java``` 命令执行。

##更多信息：

 - [Java 维基页面](http://en.wikipedia.org/wiki/Java_%28programming_language%29)
 - [JDK 维基页面](http://en.wikipedia.org/wiki/Java_Development_Kit)
 - [JRE 维基页面](http://en.wikipedia.org/wiki/Java_virtual_machine#Execution_environment)
 - [Oracle 的 Java 下载页面](http://www.oracle.com/technetwork/java/javase/downloads/index.html)

##开发Java常用的IDE
 
 - [Eclipse IDE](https://eclipse.org/downloads/packages/eclipse-ide-java-developers/lunasr1)
 - [NetBeans IDE](https://netbeans.org/downloads/)
 - [IntelliJ IDEA](http://www.jetbrains.com/idea/)
 - [Spring Tool Suite](http://spring.io/tools)（基于 Eclipse，包含用于 [Spring](http://stackoverflow.com/questions/tagged/spring) 的插件）
 - [JDeveloper IDE](http://www.oracle.com/technetwork/developer-tools/jdev/overview/index.html)
 - [Android Studio](http://developer.android.com/sdk/index.html)（基于 IntelliJ IDEA，主要用于 [android](http://stackoverflow.com/questions/tagged/android) 项目开发）
 - [BlueJ](http://www.bluej.org/)

##初学者资源
 
 - [The Java Tutorials](http://docs.oracle.com/javase/tutorial/) - 从在 Windows/Linux/Mac 上的 scratch 开始，覆盖大部分标准库。
 - [Generics](http://docs.oracle.com/javase/tutorial/java/generics/)
 - [Coding Bat (Java)](http://codingbat.com/java) - 学习部分基础之后，通过 Coding Bat 磨练和完善你的 Java 技术。
 - [Java 编程规范](http://www.oracle.com/technetwork/java/javase/documentation/codeconvtoc-136057.html)
 - [Stanford Java 视频课程](https://www.youtube.com/playlist?list=PLBD5381FE500534C0)
 - [Udemy Java 免费课程](https://www.udemy.com/java-tutorial)
 - [Edx 课程：Java 编程导论](https://www.edx.org/course?search_query=java)

##日常帮助资源
 
 - [Java SE 文档](http://www.oracle.com/technetwork/java/javase/documentation/index.html)
 - [Java 7 API 参考手册](http://docs.oracle.com/javase/7/docs/api/)
 - [Java 8 API 参考手册](http://docs.oracle.com/javase/8/docs/api/)

##进阶资源

 - [Java 语言与虚拟机说明](http://docs.oracle.com/javase/specs/)
 - [其他可以在 JVM 上与 Java 混合使用的开发语言](http://en.wikipedia.org/wiki/List_of_JVM_languages)

##免费 Java 编程图书与资源

 - [《Linux 开发 Java 应用》（Carl Albing 与 Michael Schwarz 合著，PDF）](http://ptgmedia.pearsoncmg.com/images/013143697X/downloads/013143697X_book.pdf)
 - [《如何像一名电脑科学家一样思考》](http://greenteapress.com/thinkapjava/)
 - [《Spring IO Guides》](http://spring.io/guides)
 - [《The Java EE7 Tutorial》（PDF）](http://docs.oracle.com/javaee/7/JEETT.pdf)
 - [《Java Thin-Client Programming》](http://www.redbooks.ibm.com/redbooks/SG245118.html)
 - [《Oracle's Java Tutorials》](http://docs.oracle.com/javase/tutorial/)
 - [《Thinking in Java》](http://www.mindview.net/Books/TIJ/)
 - [《OSGi in Practice》（PDF）](http://njbartlett.name/files/osgibook_preview_20091217.pdf)
 - [《Category wise tutorials - J2EE》](http://www.mkyong.com/)
 - [《Java Example Codes and Tutorials - J2EE》](http://roseindia.net/java/)
 - [《Java Design Pattern Video Training》](https://www.udemy.com/java-design-patterns-tutorial/)

##常见问题

人们在 Java 主题下经常询问的问题：

通用：
 
 - [Java 与 JavaScript 有什么不同](http://stackoverflow.com/questions/245062/whats-the-difference-between-javascript-and-java)
 - [我如何将自己的 Java 程序转换为 .exe 文件](http://stackoverflow.com/questions/147181/how-can-i-convert-my-java-program-to-an-exe-file)

环境变量：
 
 - [在环境变量中设置多种 jar 包](http://stackoverflow.com/questions/219585/setting-multiple-jars-in-java-classpath/219801#219801)

```String```，```StringBuilder``` 与 ```toString```：
 
 - [在 Java 中如何比较字符串？](http://stackoverflow.com/questions/513832/how-do-i-compare-strings-in-java) 
 - [Java 中的 StringBuilder 与 StringBuffer](http://stackoverflow.com/questions/355089/stringbuilder-and-stringbuffer-in-java)
 - [为什么当我在自己的 Java 项目中打印时得到 ```SomeType@2f92e0f4```？](http://stackoverflow.com/questions/29140402/why-do-i-get-sometype2f92e0f4-when-i-print-my-java-object)
 - [Java 中的字符串常量](http://stackoverflow.com/questions/1552301/immutability-of-strings-in-java)

```equals``` 与 ```hashCode```：
 
 - [```equals()``` 和 ```==``` 有什么不同](http://stackoverflow.com/questions/2772763/why-equals-method-when-we-have-operator)
 - [在 Java 中重写 ```equals()``` 和 ```hashCode()``` 方法](http://stackoverflow.com/questions/27581/overriding-equals-and-hashcode-in-java)

Java Platform SE API：
 
 - [使用 ```nextInt()``` 后跳过 ```nextLine()```](http://stackoverflow.com/questions/13102045/skipping-nextline-after-use-nextint)
 - [在 Java 中比较日期](http://stackoverflow.com/questions/2592501/compare-dates-in-java)
 - [Java：在迭代集合的过程中做高效地删除操作](http://stackoverflow.com/questions/223918/java-efficient-equivalent-to-removing-while-iterating-a-collection)
 - [如何排序 ```Map<Key, Value>``` 中的值](http://stackoverflow.com/questions/109383/how-to-sort-a-mapkey-value-on-the-values-in-java)
 - [什么时候使用 ```LinkedList<>``` 而不是 ```ArrayList<>```](http://stackoverflow.com/questions/322715/when-to-use-linkedlist-over-arraylist)
 - [说明 ```Arrays.asList()```](http://stackoverflow.com/questions/20538869/arrays-aslist-in-java)
 - [```HashMap``` 与 ```Hashtable``` 之间的区别](http://stackoverflow.com/questions/40471/differences-between-hashmap-and-hashtable)

泛型：
 
 - [```List<Dog>``` 是 ```List<Animal>``` 的子类吗？为什么 Java 的泛型不支持隐式多态?](http://stackoverflow.com/questions/2745265/is-listdog-a-subclass-of-listanimal-why-arent-javas-generics-implicitl)
 - [Java 泛型：PECS 是什么？](http://stackoverflow.com/questions/2723397/java-generics-what-is-pecs)
 - [原型是什么？为什么我们不应使用？](http://stackoverflow.com/questions/2770321/what-is-a-raw-type-and-why-shouldnt-we-use-it)
 - [如何创建一个泛型数组？](http://stackoverflow.com/questions/529085/how-to-create-a-generic-array-in-java)

类与对象：
 
 - [Java 是按引用传递的吗？](http://stackoverflow.com/questions/40480/is-java-pass-by-reference)
 - [Java ```enum``` 对比 ```public static final```字段的类有何优势？](http://stackoverflow.com/questions/9969690/whats-the-advantage-of-a-java-enum-versus-a-class-with-public-static-final-fiel)
 - [public，protected，private 与 default 之间有什么区别](http://stackoverflow.com/questions/215497/in-java-whats-the-difference-between-public-default-protected-and-private)

算法与规范：
 
 - [为什么我不能正确地打印一个 double 类型？](http://stackoverflow.com/questions/4937402/moving-decimal-places-over-in-a-double)
 - [为什么整数做除法运算会返回 0？](http://stackoverflow.com/questions/7220681/division-of-integers-in-java)
 - [Java 的 ```+=``` 操作](http://stackoverflow.com/questions/8710619/java-operator)

调试：
 
 - [```NullPointerException``` 是什么，我应该如何修复？](http://stackoverflow.com/a/24100776/829571)
 - [堆栈追踪是什么？我应该如何使用才能调试自己的应用错误？](http://stackoverflow.com/questions/3988788/what-is-a-stack-trace-and-how-can-i-use-it-to-debug-my-application-errors)
 - [我应该如何避免检查 null？](http://stackoverflow.com/questions/271526/how-to-avoid-null-statements-in-java)
 - [为什么会出现 ```NoClassDefFoundError``` 错误？](http://stackoverflow.com/questions/34413/why-am-i-getting-a-noclassdeffounderror-in-java)
 - [Java 中的 ```NoSuchMethodError```](http://stackoverflow.com/questions/2647154/java-package-project-nosuchmethod-error)

```Thread``` 与多线程：
 
 - [```java.lang.Thread.interrupt()``` 做了什么？](http://stackoverflow.com/questions/3590000/what-does-java-lang-thread-interrupt-do)
 - [无法通过打印语句查看循环中的变量改变](http://stackoverflow.com/questions/25425130/loop-doesnt-see-changed-value-without-a-print-statement)
 - [```implements Runnable``` 对比 ```extends Thread```](http://stackoverflow.com/questions/541487/implements-runnable-vs-extends-thread)

与操作系统交互：
 
 - [为什么 ```Runtime.exec(String)``` 只在一些命令下产生作用？](http://stackoverflow.com/questions/31776546/why-does-runtime-execstring-work-for-some-but-not-all-commands/31776547)

(提交者们，请仅仅列出经常被询问的问题。)

聊天室

 - [Stack Overflow 的 Java 聊天室](http://chat.stackoverflow.com/rooms/139/java)
 - [java-and-android-era](http://chat.stackoverflow.com/rooms/19132/java-and-android-era)