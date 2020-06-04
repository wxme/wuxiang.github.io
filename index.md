## Java面试题汇总

### Java基础

1. equals与==的区别

   equals:在Object.class类中由==实现,在其他重写equals方法中会比较hashcode,也会==

   ==:判断两个对象的内存地址

2. final, finally, finalize 的区别

   final:关键字,修饰类表示该类不能被继承,修饰方法表示不能被重写,修饰字段表示在初始化之后不能改变,但如果修饰的是引用,引用对应的值可以改变

   finally:try-catch异常处理块中的一部分,表示在经过try块之后无论异常与否都会进入finally块,例如:流的关闭

   finalize:Object中的方法,在GC启动时,回收该类时会调用该方法,人工调用该方法提醒GC回收该类时不一定被回收

3. 重载和重写的区别

   重载:多个方法之间方法名相同,参数类型或参数数量不同

   重写:子类中覆盖父类的方法,重写该方法,每次调用子类该方法

4. 两个对象的hashCode()相同，则 equals()是否也一定为 true？

   不一定,两个不同内存地址的对象的hashCode()可能相同,在equals()中不仅会比较hashcode还会比较内存地址

   相反equals()相同,hashCode()一定相同

5. 抽象类和接口有什么区别

   抽象类:子类使用extend继承,只能继承一个父类,有已实现的方法,和未实现的抽象方法,子类继承需要实现抽象方法

   接口:子类通过implement继承,可继承多个接口,全是未实现的抽象方法,java8之后新增default修饰的已实现的方法

6. BIO、NIO、AIO 有什么区别？

7. String，Stringbuffer，StringBuilder的区别

8. JAVA中的几种基本数据类型是什么，各自占用多少字节呢

   | byte | boolean | short | char | Integer | float | long | double |
   | :--: | ------- | ----- | ---- | ------- | ----- | ---- | ------ |
   |  1   | 1       | 2     | 2    | 4       | 4     | 8    | 8      |

9. Comparator与Comparable有什么区别？

10. String类能被继承吗，为什么。

    不能,被final修饰

11. 说说Java中多态的实现原理

12. Java泛型和类型擦除

13. int和Integer 有什么区别，还有Integer缓存的实现

    int是基本数据类型不是对象,Integer是int的封装对象,integer缓存的是数组,默认-128~127

    在使用valueOf()生成Integer对象时,如果值在缓存中就直接返回缓存中的Integer对象否则就生成一个新的对象

14. 说说反射的用途及实现原理，Java获取反射的三种方法

    ```java
    Class<?> clazz = Class.forName();
    Class<?> clazz = user.getClass();
    Class<?> clazz = User.class;
    ```

15. 面向对象的特征

    封装:将属性和行为封装在类中,然后提供对外方法供访问

    继承:子类继承父类的非私有字段和方法

    多态:子类的定义引用可以指向父类或父接口

16. &和&&的区别

    & : 两个都会计算,为运算符进行按位与计算

    && :短路与,第一个表达式为false就不会计算第二个

17. Java中IO流分为几种?

    输入流和输出流,字节流和字符流

18. 讲讲类的实例化顺序，比如父类静态数据，构造函数，子类静态数据，构造函数。

19. Java创建对象有几种方式

    ```java
    // 直接new
    User user = new User();
    // 使用反射
    User user = (User) Class.forName("user").newInstance();
    User user = User.class.newInstance();
    ```

20. 如何将GB2312编码的字符串转换为ISO-8859-1编码的字符串呢？

21. 守护线程是什么？用什么方法实现守护线程

    守护线程是一种特殊的线程,生命周期存在于被守护的线程中

    Thread.setDaemon(true);

22. notify()和 notifyAll()有什么区别？

    notify():唤醒还在等待当前锁的一个线程

    notifyAll():唤醒在等待当前锁的所有线程,然后所有线程竞争当前锁

23. Java语言是如何处理异常的，关键字throws、throw、try、catch、finally怎么使用？

24. 谈谈Java的异常层次结构

25. 静态内部类与非静态内部类有什么区别

    获取实例:静态内部类直接使用外部类名加内部类名实例化,非静态内部类名需要外部类实例创建新内部类实例

    变量:静态内部类只能访问静态变量,非静态内部类可以使用外部类的所有变量

26. String s与new String与有什么区别

    String s = "s"; // 先去常量池查有没有该字符串,有就直接返回地址,没有就在堆中创建一块内存和常量池中放入该字符串并返回堆内存地址

    String s = new String("s"); //先在堆中创建一块内存地址,该内存地址指向存在常量池的字符串的地址

27. 反射中，Class.forName和ClassLoader的区别

    Class.forName()会初始化,ClassLoader不会,参考Driver类

28. JDK动态代理与cglib实现的区别

    JDK动态代理需要目标类继承invocationHandler,CGLIB不需要目标类继承接口,修改字节码生成被代理类的子类覆盖方法实现

29. error和exception的区别，CheckedException，RuntimeException的区别。

30. 深拷贝和浅拷贝区别

    深拷贝是两个对象,浅拷贝是只拷贝引用,指向的对象一致

31. JDK 和 JRE 有什么区别？

32. String 类的常用方法都有那些呢？

33. 谈谈自定义注解的场景及实现

34. 说说你熟悉的设计模式有哪些？

    单例模式,工厂模式,门面模式,装饰器模式,建造者模式,代理模式

35. 抽象工厂和工厂方法模式的区别？

36. 什么是值传递和引用传递？

37. 可以在static环境中访问非static变量吗？

38. Java支持多继承么,为什么？

    不能,钻石问题

39. 用最有效率的方法计算2乘以8？

    2 << 2

40. 构造器是否可被重写？

    不能

41. char型变量中能不能存贮一个中文汉字，为什么？

    可以,char是以ASCII码存储,中文也是ASCII码存储

42. 如何实现对象克隆？

    继承Cloneable接口,重写Clone方法

    继承Serializable接口,序列化克隆对象

43. object中定义了哪些方法？

    toString(),hashCode(),equals(),clone()等

44. hashCode的作用是什么？

    hashCode便于查询快捷,可以散列数据结构中定位对象存储位置

    用于比较,equals相等则hashCode一定相等

    hashCode相同不一定相等,只能说明在散列结构中存储的位置一样

45. for-each与常规for循环的效率对比

46. 写出几种单例模式实现，懒汉模式和饿汉模式区别

    懒汉模式:在初始化的时候就实例化一个对象

    饿汉模式:在第一次使用该对象的时候才实例化

47. 请列出 5 个运行时异常。

    NPE,ArrayIndexOutOfBoundsException,ClassNotFoundException,IllegalArgumentException,SQLException

48. 2个不相等的对象有可能具有相同的 hashcode吗？

    可能

49. 访问修饰符public,private,protected,以及default的区别？

50. 谈谈final在java中的作用？

    修饰类:不能被继承

    修饰方法:不能被复写

    修饰字段:初始化后不能修改,如果是引用则指向的对象可以修改

51. java中的Math.round(-1.5) 等于多少呢？

    -1

52. String属于基础的数据类型吗？

    不是,底层是char[]

53. 如何将字符串反转呢？

    反向遍历字符数组,使用Stringbuilder的reverse方法

54. 描述动态代理的几种实现方式，它们分别有什么优缺点

    JDK动态代理:需要继承InvocationHandler实现invoke()方法

    CGLIB动态代理:在字节码层面实现,无需继承类,通过修改字节码生成被代理类的子类并覆盖方法实现

55. 在自己的代码中，如果创建一个java.lang.String类，这个类是否可以被类加载器加载？为什么。

    不可以,双亲委派机制,加载类时类加载器会向上使用父加载器加载,此时BootStrap加载器是加载本地代码中的String类

    所以双亲委派机制是为了应用的稳定性和安全性

56. 谈谈你对java.lang.Object对象中hashCode和equals方法的理解。在什么场景下需要重新实现这两个方法。

    当对象中有复杂属性的时候,在比较的时候需要考虑内部属性的影响就需要重写equals方法,重写equals方法时用到hashcode时需要重写hashCode()

57. 在jdk1.5中，引入了泛型，泛型的存在是用来解决什么问题。

58. 什么是序列化，怎么序列化，反序列呢？

    <https://blog.csdn.net/weixin_39723544/article/details/80527550>

59. java8的新特性。

    lambda表达式,Stream流,Calendar类,LocalDate类

60. 匿名内部类是什么？如何访问在其外面定义的变量呢？

61. break和continue有什么区别？

    continue是结束当前此循环进入下次循环,break是跳出循环

62. String s = "Hello";s = s + " world!";这两行代码执行后，原始的 String 对象中的内容是否会改变？

    不会,s只是改变了引用

63. 怎样将GB2312编码的字符串转换为ISO-8859-1编码的字符串？

    new String(s.getBytes("GB2312"),"ISO-8859-1");

64. try-catch-finally-return执行顺序

    try-catch-return-finally

65. Java 7新的 try-with-resources语句，平时有使用吗

66. 简述一下面向对象的”六原则一法则”。

67. switch是否能作用在byte 上，是否能作用在long 上，是否能作用在String上？

    不能使用long,float,double,boolean等不确定精度的类型

68. 数组有没有length()方法？String有没有length()方法？

    数组有length属性,String有length()方法

69. 是否可以从一个静态（static）方法内部发出对非静态（non-static）方法的调用？

    可以,通过类去调用

70. String s = new String("jay");创建了几个字符串对象？

    如果常量池中不存在该字符串:在常量池中创建字符串,在堆内存中创建指向字符串的内存

    如果常量池中存在该字符串就只会在堆内存中创建一个引用

71. 匿名内部类是否可以继承其它类？是否可以实现接口？

    不可以

72. 我们能将int强制转换为 byte类型的变量吗？如果该值大于byte 类型的范围，将会出现什么现象？

    能强制转换,会溢出,byte的范围在-128~127,如果将值为128的int类型转换为byte类型,此时byte类型为-128

73. float f=3.4;正确吗？

    float f = 3.4F;

74. 你能写出一个正则表达式来判断一个字符串是否是一个数字吗？

75. Reader和InputStream区别？

    Reader读取的字符,InputStream读取的是字节

76. 列举出JAVA中6个比较常用的包

77. JDK 7有哪些新特性

78. 同步和异步有什么区别？

79. 实际开发中，Java一般使用什么数据类型来代表价格？

80. 64 位 JVM 中，int 的长度是多数？

    8个字节,32位

81. java8的新特性

    lambda表达式,Stream流,LocalDate类,Calendar类

82. 字节流与字符流的区别

    字节流的处理单位为字节,字符流处理单位为两个字节的Unicode编码,JVM将字节转换为字符,然后读取

83. Java 事件机制包括哪三个部分？分别介绍下。

84. 为什么等待和通知是在 Object 类而不是 Thread 中声明的？

85. 每个对象都可上锁，这是在 Object类而不是 Thread 类中声明，为什么呢？

86. 为什么char 数组比Java中的 String 更适合存储密码？

87. 如何使用双重检查锁定在 Java 中创建线程安全的单例？

88. 如果你的Serializable类包含一个不可序列化的成员，会发生什么？你是如何解决的？

    会报NoSerializableException,将成员类继承Serializable接口或者设置成员变量用trancient修饰

89. 什么是serialVersionUID ？如果你不定义这个, 会发生什么？

90. Java 中，Maven 和 ant，gradle 有什么区别？

91. 常见的序列化协议有哪些

92. @transactional注解在什么情况下会失效，为什么。

93. Java 中，DOM 和SAX 解析器有什么不同？

94. 数组在内存中如何分配；

95. 什么是 Busy spin？我们为什么要使用它？

96. Java 中怎么获取一份线程 dump 文件？

97. 父类的静态方法能否被子类重写

    不能

98. 什么是不可变对象

99. 如何正确的退出多层嵌套循环？

100. SimpleDateFormat是线程安全的吗?你一般怎么格式化

     不是,放在ThreadLocal里使用

101. 抽象类必须要有抽象方法吗？

     不是

102. 怎么实现动态代理？有哪些应用

     JDK动态代理:代理类需要继承InvocationHandler

     CGLIB动态代理:通过修改字节码继承该类覆盖方法实现

103. 什么是内部类？内部类的作用

104. 泛型中extends和super的区别

105. 内部类有几种，在项目中的有哪些应用

     成员内部类:在对象中存在的内部类

     静态内部类:用static修饰的成员内部类,不能访问非静态变量

     匿名内部内:Interface i = new Interface(){};

106. utf-8编码中的中文占几个字节；int型几个字节？

     3个字节,4个字节

107. 说说你对Java注解的理解

108. Java 中 java.util.Date 与 java.sql.Date 有什么区别？

     后者是前者的子类,针对日期,获取时间戳有getTime获取,toString是格式化的日期字符串

109. 说一下隐式类型转换

110. 抽象类能使用final修饰吗

     不能,抽象类就是为了给子类继承实现抽象方法的

111. 给我一个符合开闭原则的设计模式的例子

     工厂模式

112. Files的常用方法都有哪些

113. Java 中，Serializable与Externalizable 的区别？

     Externalizable继承自Serializable接口,有read的write方法,类可是继承该接口,实现两个方法,序列化需要的字段

114. Java锁有哪些种类，它们都有哪些区别

115. 抽象的方法是否可同时是静态的）,是否可同时是本地方法），是否可同时被 synchronized 修饰？

116. 一个”.java”源文件中是否可以包含多个类（不是内部类）？有什么限制？

117. 说说代理的实现原理

     代理类中继承或注入被代理类,在代理方法中使用被代理类的方法,然后在被代理方法前后加上处理操作

     最后执行代理类中的方法

118. 了解哪设计模式，举例说说在jdk源码哪些用到了你说的设计模式

     <https://blog.csdn.net/baiye_xing/article/details/76427717>

119. 什么是B/S架构？什么是C/S架构

     Browser-Server和Client-Server

120. Java有那些开发平台呢？

121. Java内部类为什么可以访问到外部类呢？

     通过反编译得知内部内持有外部内的引用

122. Java支持的数据类型有哪些？什么是自动拆装箱呢？

     byte,sort,char,int,long,float,double,boolean

123. 创建线程有几种不同的方式

     继承Thread类

     继承Runable接口,无返回值不可抛异常

     继承Callable接口实现Call()可抛异常,有返回值

124. hashCode()和equals()方法的重要性体现在什么地方？

125. 如何通过反射获取和设置对象私有字段的值？

     先获取当前对象的class对象,在通过class对象获取全部字段,设置字段访问属性为true,比较字段名设置字段属性值即可

126. 如何通过反射调用对象的方法？

     先获取当前对象的class对象,然后获取当前对象指定方法,执行method的invoke()方法,传入当前对象的实例和参数,invoke返回值就是方法返回值

127. 简述一下面向对象的"六原则一法则"

128. Java 对象不使用时为什么要赋值为 null？

     方便GC回收

129. 什么时候用断言（assert）？

130. AJAX请求为什么不安全？

131. 一个Java字符串中到底能有多少个字符?

     2^31 - 1

132. StringBuilder为什么线程不安全？

     多线程操作时拼接顺序可能改变,所以在StringBuffer中使用Synchronized修饰同步方法

133. 深克隆和浅克隆

     浅克隆:只克隆引用,指向的内存地址还是同一个

     深克隆:开辟新的内存地址,新的引用指向新的内存地址

134. 聊一聊设计模式的基本原则

135. Java 能否自定义一个类叫 java.lang.System？

     可以,只不过不能被加载到,由于双亲委派机制

136. Java中的两种异常类型是什么？他们有什么区别？

     Error和Exception

137. Java中Exception和Error有什么区别？

138. throw和throws有什么区别？

     throw在方法体中使用,throws在方法上使用

139. 异常处理完成以后，Exception对象会发生什么变化？

140. 什么是RMI？

     远程方法调用:一种实现远程过程调用的API

141. 解释下Serialization和Deserialization。

     序列化和反序列化,将java对象以某种序列化协议比如以字节流写入到文件中这是序列化,从文件中读取字节流到对象叫返序列化,主要目的在于java对象的持久化

142. 环境变量Path和ClassPath的作用是什么？如何设置这两个环境变量？

143. 字符型常量和字符串常量的区别

     char和String,String底层是char[]

144. 构造器Constructor是否可被override

     不可以

145. 什么是方法的返回值？返回值在类的方法里的作用是什么？

146. 一个类的构造方法的作用是什么？若一个类没有声明构造方法，改程序能正确执行吗？为什么？

147. 静态方法和实例方法有何不同？

148. 对象的相等与指向他们的引用相等，两者有什么不同？

149. 用 Java 写一个线程安全的单例模式

     饿汉或者懒汉单例在对象实例化的时候用Synchronized加锁即可

150. 我能在不进行强制转换的情况下将一个 double值赋值给 long类型的变量吗？

151. java 枚举类型是否可以继承 (final)？

152. Cloneable 接口实现原理？

     Object的Clone本地方法会判断对象是否继承Cloneable接口,没有则会抛出NoCloneableException

153. 继承和聚合的区别？

154. 能用Java覆盖静态方法吗？如果我在子类中创建相同的方法是编译时错误？

     不能覆盖,在子类中创建相同的方法是新方法不会编译错误,因为调用时需要方法所在类加方法使用

155. 什么是Java程序的主类？应用程序和小程序的主类有何不同？

156. instanceof 工作中使用过吗？

     判断是否为某个类或某个类的子类

157. Java自带线程池判断线程池是否已经结束运行的方法叫什么

158. 成员变量与局部变量的区别有那些？

159. 创建一个对象用什么运算符? 对象实体与对象引用有何不同?

160. 一行Java代码是如何执行的？

### Java 集合

1. Arraylist与LinkedList区别

   ArrayList底层为数组,顺序存储,写少查多

   LinkedList底层为链表,无序存储,写多查少

2. Collections.sort和Arrays.sort的实现原理

   前者调用List.sort()使用Arrays.sort

3. HashMap原理，java8做了什么改变

4. List 和 Set，Map 的区别

   List: 列表,可重复存储元素

   Set: 集合,不可重复元素

   Map: k-v键值对

5. poll()方法和 remove()方法的区别？

   两个方法都是弹出一个元素,对于空队列时的处理不同,poll返回null,remove抛出异常

6. HashMap，HashTable，ConcurrentHash的共同点和区别

7. 写一段代码在遍历 ArrayList 时移除一个元素

   使用iterator迭代器

8. Java中怎么打印数组？

   Arrays.toString()和遍历打印

9. TreeMap底层？

   底层是红黑树,在插入时进行计算排序,有自然排序和定制排序,需要key继承Comparable接口,定制排序需要传入Comparator对象

10. HashMap 的扩容过程

    扩容两倍

    判断桶位置是否有元素,没有元素就插入,判断是否达到桶阈值,达到就扩容

    如果有元素就判断链表还是树,如果链表元素超过8就树化

11. HashSet是如何保证不重复的

    HashSet底层使用HashMap中的key存储值,使用hash和equals()保证不重复

12. HashMap 是线程安全的吗，为什么不是线程安全的？死循环问题？

    不安全,7之前链表扩容时使用头插法容易导致死循环

13. LinkedHashMap的应用，底层，原理

    LinkedHashMap解决HashMap遍历顺序与插入顺序不一致问题

    底层继承HashMap,又额外维护一个双向链表,保持顺序一致

14. 哪些集合类是线程安全的？哪些不安全？

    ConcurrentHashMap,Vector,CopyOnWriteArrayList/Set/Map

15. ArrayList 和 Vector 的区别是什么？

    Vector是线程安全的,使用synchronized修饰方法

16. Collection与Collections的区别是什么？

    Collection是集合顶级接口

    Collections是工具类,有基本集合操作方法如sort

17. 如何决定使用 HashMap 还是TreeMap？

    HashMap无序但插入,删除,定位元素快

    TreeMap有序可比较

18. 如何实现数组和 List之间的转换？

    使用arrays.asList():数组转列表,再使用new ArrayList(asList);

    list.toArray():列表转数组

19. 迭代器 Iterator 是什么？怎么用，有什么特点？

20. Iterator 和 ListIterator 有什么区别？

21. 怎么确保一个集合不能被修改？

22. 快速失败(fail-fast)和安全失败(fail-safe)的区别是什么？

23. 什么是Java优先级队列(Priority Queue)？

24. JAVA8的ConcurrentHashMap为什么放弃了分段锁，有什么问题吗，如果你来设计，你如何设计。

25. 阻塞队列的实现，ArrayBlockingQueue的底层实现？

26. Java 中的 LinkedList是单向链表还是双向链表？

27. 说一说ArrayList 的扩容机制吧

    1.5倍扩容,使用Arrays.copyOf()复制对象

28. HashMap 的长度为什么是2的幂次方，以及其他常量定义的含义~

    便于进行计算,还有桶的算法是用hash & (length - 1)来做运算

29. ConcurrenHashMap 原理？1.8 中为什么要用红黑树？

    对HashMap的并发处理,对写操作的对象加同步锁

30. ArrayList的默认大小

    10

31. 为何Collection不从Cloneable和Serializable接口继承？

    接口尽量简单,将需要的接口有子类实现更好,如ArrayList和HashSet都继承了这两个接口

32. Enumeration和Iterator接口的区别？

33. 我们如何对一组对象进行排序？

    手写排序或者使用Collections.sort方法

34. 当一个集合被作为参数传递给一个函数时，如何才可以确保函数不能修改它？

    使用不变集合,

35. 说一下 HashSet 的实现原理？

36. Array 和 ArrayList 有何区别？

37. 在 Queue中poll()和 remove()有什么区别？

    remove返回poll的结果都是弹出队列一个值并删除,如果队列为空,remove会抛出异常,poll返回null

38. ArrayList 如何删除重复的元素或者指定的元素；

    使用iterator迭代器遍历

39. 讲讲红黑树的特点？

    红黑树是特殊的搜索二叉树

    红黑树有红黑节点

    红黑树根节点和子节点是黑色

    红节点儿子都是黑节点

    每条路径的黑节点数相同

40. Java集合类框架的最佳实践有哪些？

    定义集合时给集合赋初始容量,最好是2的幂

    遍历有删除时使用迭代器遍历

    使用泛型控制对象

    当集合为返回值时尽量返回空集合而不是null

41. Enumeration接口和Iterator 接口的区别有哪些？

42. HashSet和TreeSet有什么区别？

    HashSet是无序的,TreeSet有序且可比较

43. Set里的元素是不能重复的，那么用什么方法来区分重复与否呢? 是用==还是equals()?

    使用hash和equals

44. 说出ArrayList,LinkedList的存储性能和特性

    ​			底层		存储			用途

    ArrayList		数组		顺序存储		读多写少

    LinkedList	链表		无序存储		读少写多

45. Java中HashMap的key值要是为类对象则该类需要满足什么条件？

    重写该类的hashCode()和equals()方法

46. ArrayList集合加入1万条数据，应该怎么提高效率

    预先确定容量,不用扩容耗费时间和性能

47. 如何对Object的list排序

    使用Collections.sort()方法

48. ArrayList 和 HashMap 的默认大小是多数？

    10 和 16

49. 有没有有顺序的Map实现类，如果有，他们是怎么保证有序的

    treeMap,继承SortedMap,key需要继承Comparable接口,有自然排序和定制排序传入comparator对象

50. HashMap是怎么解决哈希冲突的

    链表加红黑树

### Java 并发 && 多线程

1. synchronized 的实现原理以及锁优化？

   实现原理:

   ​	同步代码块监视器为对象,方法为当前对象实例,静态方法为对象的class对象

   ​	同步代码块:在字节码层面通过monitorenter和monitorexit指令通过监听器对象去获取锁和释放锁

   ​	同步方法:依靠方法上的修饰符ACC_SYCHRONIZED访问标志获取monitor然后在方法执行完成后再释放

   锁优化:偏向锁 -> 轻量级锁 -> 重量级锁

   ​	偏向锁:锁不存在多线程进程且总是由统一线程反复获得,该同步代码块中的对象中的对象头和栈帧的锁记录中存储锁偏向的线程,以后该线程在进入和退出同步块不需要进行CAS操作,只需要简单测试对象头中是否存储当前线程的偏向锁,如果失败则再次测试偏向锁的标识是否设置成1,没有则使用CAS竞争锁,有则将对象头的偏向锁指向当前线程

   若锁有竞争关系则进入轻量级锁

   ​	轻量级锁

   ​	

2. ThreadLocal原理，使用注意点，应用场景有哪些？

   线程本地变量,给每个线程创建独立的副本,每个副本之间不会互相影响

   Spring的事务管理底层就是使用ThreadLocal存储事务数据的

   Thread类中有ThreadLocalMap类,ThreadLocalMap类中存储以当前ThreadLocal为Key,变量为value的键值对

3. synchronized和ReentrantLock的区别？

   ![img](https://p0.meituan.net/travelcube/412d294ff5535bbcddc0d979b2a339e6102264.png)

4. 说说CountDownLatch与CyclicBarrier 区别

5. Fork/Join框架的理解

6. 为什么我们调用start()方法时会执行run()方法，为什么我们不能直接调用run()方法？

   run只是业务逻辑代码,start()会调用本地方法start0()进行创建线程

7. Java中的volatile关键是什么作用？怎样使用它？在Java中它跟synchronized方法有什么不同？volatile 的实现原理

   volatile的作用是确保所有线程看到的变量值是一致的

   volatile是轻量级的synchronize

   处理器是不直接与内存通信,先写到缓冲行,然后缓冲行写入内存,但是时间不确定是否实时,如果写入的是volatile值在写指令后还会有一条lock开头的指令,会将这个变量所在的缓冲行写入内存

   在多处理器下,每个处理器的缓冲行需要实现缓存一致性操作即每个处理器通过嗅探在总线上的数据确保自己缓存的值是不是最新(自己缓存行的内存地址是否被修改)

8. CAS？CAS 有什么缺陷，如何解决？

   CompareAndSwap

   ABA问题:当线程t1修改值A到B,再从B到A,此时线程t2去修改也是成功的 -> 结合乐观锁加版本号或者时间戳

   多线程抢占同一资源时,线程做自旋会消耗CPU资源 -> 设置自旋超时时间或者自旋次数

   多变量共享一致性问题:CAS操作针对一个变量的,多变量可加锁或者封装对象实现

9. 如何检测死锁？怎么预防死锁？死锁四个必要条件

   死锁的四个必要条件:

   互斥条件:一个线程只能保持一个资源,且其他线程访问该资源的时候只能等待

   请求与保持条件:每个线程都保持其他线程想访问的资源且自己请求的资源被其他线程占用

   不可剥夺条件:线程保持的资源不可被其他线程强行获取,只能靠该线程自己释放

   循环等待条件:若干线程形成首尾相接的循环等待资源的关系

   预防:破坏除死锁的四个条件即可

10. 如果线程过多,会怎样?

11. 说说 Semaphore原理？

12. AQS组件，实现原理

13. 假设有T1、T2、T3三个线程，你怎样保证T2在T1执行完后执行，T3在T2执行完后执行？

14. LockSupport作用是？

15. Condition接口及其实现原理

16. 说说并发与并行的区别?

17. 为什么要用线程池？Java的线程池内部机制，参数作用，几种工作阻塞队列，线程池类型以及使用场景

18. 如何保证多线程下 i++ 结果正确？

19. 10 个线程和2个线程的同步代码，哪个更容易写？

20. 什么是多线程环境下的伪共享（false sharing）？

21. 线程池如何调优，最大数目如何确认？

22. Java 内存模型？

23. 怎么实现所有线程在等待某个事件的发生才会去执行？

24. 说一下 Runnable和 Callable有什么区别？

    Runnable中的run方法没有返回值,不能抛出异常

    Callable中的call方法有返回值,可以抛出异常

25. 用Java编程一个会导致死锁的程序，你将怎么解决？

26. 线程的生命周期，线程的几种状态。

27. ReentrantLock实现原理

28. java并发包concurrent及常用的类

29. wait(),notify()和suspend(),resume()之间的区别

30. FutureTask是什么？

31. 一个线程如果出现了运行时异常会怎么样

32. 生产者消费者模型的作用是什么

33. ReadWriteLock是什么

34. Java中用到的线程调度算法是什么？

35. 线程池中的阻塞队列如果满了怎么办？

36. 线程池中 submit()和 execute()方法有什么区别？

37. 介绍一下 AtomicInteger 类的原理？

38. 多线程锁的升级原理是什么？

39. 指令重排序，内存栅栏等？

40. Java 内存模型 happens-before原则

41. 公平锁/非公平锁

42. 可重入锁

43. 独享锁、共享锁

44. 偏向锁/轻量级锁/重量级锁

45. 如何保证内存可见性

46. 非核心线程延迟死亡，如何实现？

47. ConcurrentHashMap读操作为什么不需要加锁？

48. ThreadLocal 如何解决 Hash 冲突？

49. ThreadLocal 的内存泄露是怎么回事？

50. 为什么ThreadLocalMap 的 key是弱引用，设计理念是？

51. 同步方法和同步代码块的区别是什么？

52. 在Java中Lock接口比synchronized块的优势是什么？如果你需要实现一个高效的缓存，它允许多个用户读，但只允许一个用户写，以此来保持它的完整性，你会怎样去实现它？

53. 用Java实现阻塞队列。

54. 用Java写代码来解决生产者——消费者问题。

55. 什么是竞争条件？你怎样发现和解决竞争？

56. 为什么我们调用start()方法时会执行run()方法，为什么我们不能直接调用run()方法？

57. Java中你怎样唤醒一个阻塞的线程？

58. 什么是不可变对象，它对写并发应用有什么帮助？

59. 你在多线程环境中遇到的共同的问题是什么？你是怎么解决它的？

60. Java 中能创建 volatile数组吗

61. volatile 能使得一个非原子操作变成原子操作吗

62. 你是如何调用 wait（）方法的？使用 if 块还是循环？为什么？

63. 我们能创建一个包含可变对象的不可变对象吗？

64. 在多线程环境下，SimpleDateFormat是线程安全的吗

65. 为什么Java中 wait 方法需要在 synchronized 的方法中调用？

66. BlockingQueue，CountDownLatch及Semeaphore的使用场景

67. Java中interrupted 和 isInterruptedd方法的区别？

68. 怎么检测一个线程是否持有对象监视器

69. 什么情况会导致线程阻塞

70. 如何在两个线程间共享数据

71. Thread.sleep(1000)的作用是什么？

72. 使用多线程可能带来什么问题

73. 说说线程的生命周期和状态?

74. 什么是上下文切换

75. Java Monitor 的工作机理

76. 按线程池内部机制，当提交新任务时，有哪些异常要考虑。

77. 线程池都有哪几种工作队列？

78. 说说几种常见的线程池及使用场景?

79. 使用无界队列的线程池会导致内存飙升吗？

80. 为什么阿里发布的 Java开发手册中强制线程池不允许使用 Executors 去创建？

81. Future有缺陷嘛？

### JVM 篇

1. 什么情况下会发生栈内存溢出。什么时候发生堆溢出？你是怎么排错的？
2. JVM怎么判断对象是可回收对象？有哪些方法。
3. JVM的内存结构，新生代与老年代的比例，Eden和Survivor比例。
4. 你知道哪几种垃圾收集器，各自的优缺点，重点讲下cms和G1，包括原理，流程，优缺点。
5. 简单说说你了解的类加载器，可以打破双亲委派么，怎么打破。
6. JVM内存为什么要分成新生代，老年代，持久代。新生代中为什么要分为Eden和Survivor。
7. JVM 出现 fullGC 很频繁，怎么去线上排查问题？
8. JVM中一次完整的GC流程是怎样的，对象如何晋升到老年代，说说你知道的几种主要的JVM参数。
9. 垃圾回收算法的实现原理。
10. JVM内存模型的相关知识了解多少，比如重排序，内存屏障，happen-before，主内存，工作内存等。
11. 说一下Java对象的创建过程
12. 你们线上应用的JVM参数配置了哪些。
13. G1和cms区别。
14. 怎么打出线程栈信息。
15. 说一下类加载的执行过程
16. JVM垃圾回收机制，何时触发MinorGC等操作呢？
17. ZGC 垃圾收集器，了解过吗
18. 对象的访问定位有哪两种方式?
19. 说一下 jvm 调优的工具？
20. 对象什么时候会进入老年代？
21. 内存泄漏和内存溢出区别？
22. 什么是tomcat类加载机制？
23. 了解逃逸分析技术吗
24. 调用System.gc()会发生什么?
25. 谈谈Minor GC条件，full GC条件
26. Stop The World 了解过吗？
27. 谈谈你认识多少种OOM？如何避免OOM?
28. 了解过JVM调优没，基本思路是什么?如何确定它们的大小呢？
29. 淘宝热门商品信息在JVM哪个内存区域
30. 字节码的编译过程
31. Java需要开发人员回收内存垃圾吗？
32. Java中垃圾回收有什么目的？什么时候进行垃圾回收？
33. System.gc()和Runtime.gc()会做什么事情？
34. 主内存与工作内存
35. 内存间交互操作
36. volatile 禁止内存重排序
37. 内存模型三大特性
38. 谈谈先行发生原则
39. JVM 堆内存溢出后，其他线程是否可继续工作？
40. 说一下JVM 常用参数有哪些？
41. VM 为什么使用元空间替换了永久代？
42. Java堆的结构是什么样子的？什么是堆中的永久代(Perm Gen space)?
43. JVM的永久代中会发生垃圾回收么？
44. 什么是字节码？采用字节码的最大好处是什么？什么Java是虚拟机？
45. MinorGC 的过程
46. CPU 占用过高如何分析
47. Serial与Parallel GC之间的不同之处？
48. WeakHashMap 是怎么工作的？
49. 解释 Java 堆空间及 GC？
50. 你能保证 GC 执行吗？
51. JVM中哪个参数是用来控制线程的栈堆栈小的?

### 数据库

1. MySQL 索引使用有哪些事项呢？

   索引失效:

   ​	查询条件包含or,可能导致索引失效

   ​	索引字段是字符串时需要用引号括起来,否发会隐式转换索引失效

   ​	like可能导致索引失效(使用"%name")

   ​	使用联合索引时,注意最左前缀原则

   ​	对索引使用内置函数

   ​	对索引进行运算

   ​	使用!=,><,not in,is null,not null时

   ​	左右连接查询时两边关联字段编码格式不一致

   ​	mysql优化器认为全表查询比索引查询快时不使用索引

   索引不适合的场景:

   ​	数据量较小不适合加索引

   ​	更新频繁的字段不适合加索引,会进行索引的维护

   ​	区分度低的字段不适合加索引,如:性别

     索引潜规则:

   ​	最左前缀原则:建立了(a,b,c)的联合索引就相当于建立了(a),(a,b),(a,b,c)三个索引

   ​	回表:聚集索引的叶子节点存储主键值和行数据,普通索引的叶子节点只存储主键值,用普通索引去查询定位到聚集索引,然后从聚集索引查询到行数据

   ​	索引数据结构(B+树)

   ​	覆盖索引:在查询索引列包含查询字段

   ​	索引下推:两个或多个条件进行查询时,会在同一条数据进行多条件查询而不是每个查询一次查出多数据依次查询

2. 说说分库与分表的设计

   ​	水平分表:以字段为依据,将一个表中的数据拆分到多个表中

   ​	水平分库:以字段为依据,将一个表中的数据拆分到多个库中

   ​	垂直分表:以表为依据,将表字段拆分到不同的表中,冗余主键关联

   ​	垂直分库:以字段为依据,将表字段拆分到不用的库中

3. 日常工作中你是怎么优化SQL的？

   对常用查询字段加索引

   只查询需要的字段

   数据量过大进行分批次进行

   优化sql结构

   分库分表

   读写分离

4. MySQL 遇到过死锁问题吗，你是如何解决的？

5. InnoDB与MyISAM的区别

6. 数据库索引的原理，为什么要用 B+树，为什么不用二叉树？

   ​	二叉树会特殊化为链表,相当于全表查询

   ​	平衡二叉树每个节点只能存储一个键值和数据,然后树的高度就会很高不利于查询

   ​	B树可以有多个节点存储多个键值和数据,树会更矮更胖

   ​	B+树相对于B树:

   ​		B+树非子节点只存储键值,而B树的节点都会存储键值和数据

   ​		B+树的子节点之间是有连接的,进行范围查询更快

7. 聚集索引与非聚集索引的区别

   聚集索引:一个表中只存在一个,聚集索引的逻辑顺序相当于数据的物理存储顺序

   非聚集索引:一个表中可存在多个,非聚集索引的逻辑顺序和物理存储顺序不一致

8. limit 100000 加载很慢的话，你是怎么解决的呢？

   采用分页加载

9. 如何选择合适的分布式主键方案呢？

10. 事务的隔离级别有哪些？MySQL的默认隔离级别是什么？

    读未提交,读以提交,可重复读,串行化(序列化),默认级别是可重复读

11. 什么是幻读，脏读，不可重复读呢？

    脏读:事务A在查询过程中查到事务B已修改但未提交的数据

    不可重复读:事务A有两个查询过程,在两个查询中间事务B修改数据并提交,事务A的两次查询结果不一致

    幻读:事务A查询到相同范围的结果集,第一次查询过后事务B新增或删除数据,然后事务A再查询就得到不一致的结果集

12. 在高并发情况下，如何做到安全的修改同一行数据？

    加锁

13. 数据库的乐观锁和悲观锁。

    悲观锁:认为每一次操作都是不安全的,所以对每一次操作都会加锁:select for update

    乐观锁:对表加加个时间戳版本号,每次进行操作时对比版本号,版本号一直才能操作成功,CAS

14. SQL优化的一般步骤是什么，怎么看执行计划（explain），如何理解其中各个字段的含义。

    先看数据量

15. select for update有什么含义，会锁表还是锁行还是其他。

    行锁,会锁住符合筛选条件的行数据

16. MySQL事务得四大特性以及实现原理

    ACID:

    原子性:要么不执行要么全执行,使用undo log,如果过程出错会使用undo log执行rollback回滚到事务执行之前的状态

    一致性:事务开始之前和事务结束以后的数据不会被破坏

    隔离性:多个事务之间是相互隔离的,不会相互影响,使用锁以及MVCC(多版本并发控制)

    持久性:事务完后之后,该事务对数据库所做的操作是持久保存的,使用redo log实现,redo log持久化之后,系统崩溃可使用redo log恢复数据

17. 如果某个表有近千万数据，CRUD比较慢，如何优化。

    分库分表,索引优化,查询优化

18. 如何写sql能够有效的使用到复合索引。

    对查询频繁的列做符合索引,支持最左前缀原则,建立(a,b,c)就相当于建立(a),(a,b),(a,b,c)

19. mysql中in 和exists的区别。

    in:先做in中的子查询,然后再做主查询,如果子查询中的数据小于主查询中的表数据使用in

    exists:先做主查询,然后再放到子查询中做判断,子查询中的数据大于主查询时使用exists

20. 数据库自增主键可能遇到什么问题。

    分库分表会出现主键冲突

    自增锁是表锁

    自增键可能用完

21. MVCC熟悉吗，它的底层原理？

    MVCC:多版本并发控制

    隐式字段:DBTRXID,记录每一行最近一次修改它的事务id

    ​		DBROLLPTR,指向回滚段的undo日志

    ​		DRROWID:自增行ID(当表中无主键和非null唯一键时)

    undo log:undo是逻辑日志,记录每个操作的相反操作以便事务回滚,如:delete -> insert,存储undo日志的地方就是回滚段,多个事务对同一数据的修改会产生多个版本,然后通过回滚指针连接一条日志链

    快照读&当前读:快照读记录数据的可见版本,不加锁,普通select都是快照读,读取当前最新数据都是当前读,加锁:

    select for update,select lock in share mode

    read view:事务执行快照读时生成的读视图,主要用来做可见性判断

    ​		事务id小于read view中的最小事务版本则可访问

    ​		事务id大于read view中的最大事务版本则不可访问

    ​		事务id在之间,则判断是否在活跃id集合内

22. 数据库中间件了解过吗，sharding_jdbc，mycat？

23. MYSQL的主从延迟，你怎么解决？

24. 说一下大表的优化方案

25. 什么是数据库连接池?为什么需要数据库连接池呢?

    数据库连接池:在内部对象池中维护一定数量的数据库连接,然后对外暴露连接获取方法和返回方法

    好处:当连接使用完后之后,以前是直接关闭连接,现在是放进连接池中等待下一次使用

26. 一条SQL语句在MySQL中如何执行的？

27. InnoDB引擎中的索引策略，了解过吗？

    最左前缀原则:查询条件最频繁的列在最左边,所以在创建组合索引时需要考虑最左匹配原则

    覆盖索引:普通索引树中可以得到查询的结果,不需要回到主键索引树中再次搜索

    索引下推:在索引遍历过程中,对索引包含的字段先做判断,直接过滤不存在的记录,减少回表次数

28. 数据库存储日期格式时，如何考虑时区转换问题？

29. 一条sql执行过长的时间，你如何优化，从哪些方面入手？

    首先用explain查看慢查询sql有没有优化建议

    然后看SQL中有没有适合建立索引的列

    看数据量大小,数据量过大尝试分库分表

30. MYSQL数据库服务器性能分析的方法命令有哪些?

31. Blob和text有什么区别？

    Blob存储二进制数据,例如图片,text是长文本字符串

32. mysql里记录货币用什么字段类型比较好？

    decimal或者number

33. Mysql中有哪几种锁，列举一下？

    共享锁(S锁):允许持锁事务读取一行,S锁与S锁兼容,其他锁类型都不兼容:select lock in share model

    排他锁(X锁):允许持锁事务更新或删除一行

    记录锁:最简单的行锁,仅锁住一行,select for update,永远加在索引上,没有会创建隐式索引

    间隙锁:加在两个索引之间的锁,或者两个索引之外的间隙,间隙锁对一个区间的数据加锁

    next-key:记录锁和间隙锁的组合,指加在某条记录以及这条记录前面间隙上的锁

34. Hash索引和B+树区别是什么？你在设计索引是怎么抉择的？

    Hash索引是单个命中数据,所以在等值查询上比B+数效率高

    B+树能进行范围查询

    B+树能进行Order By排序

    B+树能支持索引的最左前缀原则

    B+树能在使用like "%name"起到索引优化的作用,Hash无法进行模糊查询

35. mysql 的内连接、左连接、右连接有什么区别？

    内连接:只保存两张表中匹配的结果集

    左连接:保留左表所有的行,即使右表没有匹配记录

    右连接:保留右表所有的行,即时左表没有匹配记录

36. MySQL 的基础架构

    总体分为三层:

    一:连接处理,授权认证和安全等

    二:编译并优化sql

    三:存储引擎

37. 什么是内连接、外连接、交叉连接、笛卡尔积呢？

38. 说一下数据库的三大范式

    第一范式:表中每个列是最小单元不能再拆分

    第二范式:在第一范式基础上,非主键完全依赖主键,而不是依赖主键一部分

    第三范式:在第二范式基础上,非主键完全依赖主键,不能依赖其他非主键

39. mysql有关权限的表有哪几个呢？

    user，db，tablepriv，columnspriv和host

40. Mysql的binlog有几种录入格式？分别有什么区别？

    statement:记录修改数据的sql,需要记录上下文信息

    row:不记录上下文信息,保存被修改的数据

    mixed:根据情况使用statement或row

41. InnoDB引擎的4大特性，了解过吗

42. 索引有哪些优缺点？

    优点:

    ​	唯一索引标志行数据的唯一性

    ​	索引可加快数据查询速度,减少查询时间

    缺点:

     	创建和维护索引都需要时间

    ​	在进行更新操作时,需要对索引进行维护要耗费时间

    ​	索引需要占用物理内存

43. 索引有哪几种类型？

    主键索引,唯一索引,普通索引,覆盖索引,组合索引,全文索引

44. 创建索引有什么原则呢？

    最左前缀匹配原则

    频繁作为查询条件的字段作为索引

    频繁更新的字段不要作为索引

    索引列不能函数操作和计算

    创建组合索引时注意顺序,比如order by和group by

    区分度低的不要做索引,比如性别

    定义为text等的大数据类型列不要建索引

    删除少使用的索引

45. 创建索引的三种方式

    创建表的时候:key "index_name"("col_name") using btree

    alter table add index "index_name"(col_name)

    create index index_name on table (col_name)

46. 百万级别或以上的数据，你是如何删除的？

47. 什么是最左前缀原则？什么是最左匹配原则？

    最左前缀原则就是按查询频率由左向右创建索引

    当创建索引(a,b,c)时就相当于创建了(a),(a,b),(a,b,c),最左匹配原则

48. B树和B+树的区别，数据库为什么使用B+树而不是B树？

    B树的节点都存放键和值,B+树内部节点只存放键,只有叶子节点存放值

    B+树的叶子节点之间有链相连,可以进行范围查询,B树的叶子节点之间相互独立

49. 覆盖索引、回表等这些，了解过吗？

    覆盖索引:在普通索引树中可以查询得到的列,不用再次到主键索引树查询

    ​		如果一个索引包含或满足了查询字段中的字段和条件的数据

    回表:非主键数据无法查出所有列的数据只能查询到数据的主键,然后通过主键定位数据

50. B+树在满足聚簇索引和覆盖索引的时候不需要回表查询数据？

    在使用聚集索引时,可直接在对应的叶子节点获取数据

    覆盖索引是在非聚集索引查询得到数据直接返回不用去聚集索引查询

51. 什么是聚簇索引？何时使用聚簇索引与非聚簇索引

    聚集索引:聚集索引的逻辑顺序与数叶子节点的物理顺序一致

52. 非聚簇索引一定会回表查询吗？

    如果查询语句的字段全部命中了索引,就不会回表(覆盖索引)

53. 联合索引是什么？为什么需要注意联合索引中的顺序？

    组合索引是在做个列上建立索引

    因为innodb使用的最左前缀原则,所以要注意顺序

54. 什么是数据库事务？

    事务是多个操作序列组成的一个执行单元,要么全部执行,要么全不执行

55. 隔离级别与锁的关系

    读未提交:事务读不加锁,事务写阻塞其他事务写

    读已提交:

    可重复读:

    串行化:隐式转换成select for share,读加共享锁,写加排他锁

56. 按照锁的粒度分，数据库锁有哪些呢？锁机制与InnoDB锁算法

57. 从锁的类别角度讲，MySQL都有哪些锁呢？

    共享锁和排他锁,共享锁兼容共享锁,其他不能兼容

58. MySQL中InnoDB引擎的行锁是怎么实现的？

    根据索引实现的,select for update

59. 什么是死锁？怎么解决？

    多个事务之间持有同一资源,并相互请求锁定对方资源

60. 为什么要使用视图？什么是视图？

61. 视图有哪些特点？哪些使用场景？

62. 视图的优点，缺点，讲一下？

63. count(1)、count(*) 与 count(列名) 的区别？

    count(*)和count(1)包括所有列,不会忽略为列值为null的情况

    count(列名)只查询包含列名一行,会忽略列值为null的情况

64. 什么是游标？

65. 什么是存储过程？有哪些优缺点？

66. 什么是触发器？触发器的使用场景有哪些？

67. MySQL中都有哪些触发器？

68. 超键、候选键、主键、外键分别是什么？

69. SQL 约束有哪几种呢？

70. 谈谈六种关联查询，使用场景。

71. varchar(50)中50的涵义

72. mysql中int(20)和char(20)以及varchar(20)的区别

    int(20):int类型的数据,显示长度为20

    char(20):固定长度字符串,固定长度为20

    varchar(20):可变长度字符串,最长长度为20

73. drop、delete与truncate的区别

    drop删除表,delete删除指定行,truncate删除表数据保留表结构

74. UNION与UNION ALL的区别？

    union会忽略重复行,union all不会忽略重复行

75. SQL的生命周期？

76. 超大分页怎么处理？

77. 慢查询日志

78. 关心过业务系统里面的sql耗时吗？统计过慢查询吗？对慢查询都怎么优化过？

    查看是否返回不必要的字段

    查看索引是否需要建立

    用explain查看优化建议

    查看数据量,数据量过大就分库分表

79. 主键使用自增ID还是UUID，为什么？

    单机使用自增id,分布式使用uuId生成解决方案,自增id可能出现冲突

80. mysql自增主键用完了怎么办？

    如果类型为int可升级成bigint

81. 字段为什么要求定义为not null？

    查询和插入都可能在代码层出现问题

82. 如果要存储用户的密码散列，应该使用什么字段进行存储？

    类似定长字符串可使用char,使用varchar会进行处理消耗时间,也可以提高检索效率

83. 优化查询过程中的数据访问

    查看字段是否有不必要

    当查询单条数据时可加limit 1

    explain分析语句

    使用count(*)代替count(列名)

84. 如何优化长难的查询语句？有实战过吗？

85. 优化特定类型的查询语句

86. MySQL数据库cpu飙升的话，要怎么处理呢？

87. 读写分离有哪些解决方案？

88. MySQL的复制原理以及流程

89. 备份计划，mysqldump以及xtranbackup的实现原理？

90. Innodb的事务实现原理？

91. 谈谈 MySQL 的Explain

92. Innodb的事务与日志的实现方式

93. MySQL binlog的几种日志录入格式以及区别

94. 500台db，在最快时间之内重启。

95. 你是如何监控你们的数据库的？你们的慢日志都是怎么查询的？

96. 你是否做过主从一致性校验，如果有，怎么做的，如果没有，你打算怎么做？

97. 你们数据库是否支持emoji表情存储，如果不支持，如何操作？

    utf8改成utf8-mb4

98. MySQL中InnoDB引擎的行锁是通过加在什么上完成(或称实现)的？为什么是这样子的？

    索引,select for update

99. 一个6亿的表a，一个3亿的表b，通过外间tid关联，你如何最快的查询出满足条件的第50000到第50200中的这200条数据记录。

100. 数据库垂直和水平拆分

     垂直:以字段为依据,表字段拆分到多个库或表中

     水平:以数据为依据,将表数据拆分到多个表和库中

### 缓存/Redis

*缓存要素:*
*可设置缓存大小:cache size*
*失效策略:eviction police*
*监控统计:statistics*
*持久化存储:persistent store*

1. Redis用过哪些数据类型，每种数据类型的使用场景

   String:默认K-V结构

   Hash:存储散列表,等同java中的HashMap

   List:列表,可以存储重复value,有序

   Set:集合,不能存储重复value,无序

   Zset:有序集合

   特殊数据结构:

   Geo:存储地理位置信息

   Hyperloglog:基础统计,在大数据量下占用内存很小

   Bitmap:位图,只存位,使用例如打卡场景

2. Redis缓存穿透、缓存雪崩和缓存击穿原因，以及解决方案

   缓存穿透:一个不存在的key,在每次请求都会请求数据库,缓存无效

   ​	解决:使用布隆过滤器将key存在bitmap中,有该key的请求就被过滤

   ​		当请求数据库无此key的时候,在缓存中存储key-null

   缓存雪崩:在同一时间多个热点数据同时过期,此时请求都会同时落到数据库

   ​	解决:将热点数据的过期时间设置为不一致

   缓存击穿:当多个请求并发请求同一个key且该key过期时

   ​	解决:对读数据库写缓存操作加锁,使得只有一个线程操作写数据

3. 如何使用Redis来实现分布式锁，redis分布式锁有什么缺陷？

   *分布式锁特点:*
   ​	*互斥性: 同一时刻只能有一个线程持有锁*
   ​	*可重入锁: 同一个节点上的同一个线程如果获取了该锁之后能再次获取锁*
   ​	*锁超时: 超时机制,避免死锁*
   ​	*高性能和高可用: 加锁和解锁必须高效,同时需要保证高可用,防止分布式锁失败*
   ​	*具备阻塞和非阻塞性: 能及时从阻塞状态中唤醒*

   redis实现分布式锁:

   1.使用setnx + expire实现,setnx 意为 set not exists 不存在即修改,存在则失败返回0,不存在设置成功返回1

   然后锁的超时机制使用expire实现,由于这是两条指令,所以不具备原子性,所以可使用lua脚本

   value需要唯一性,如果有一个线程因为阻塞持有锁过期自动释放,然后线程从阻塞中恢复过来后持有的锁值释放锁导致此时其他持有锁的线程也释放了锁,故在释放锁的时候对value进行唯一性判断

   缺陷:当master线程持有锁,然后当key还未同步到salve就发生故障转移,下一个slave成为master,此时线程也可拥有锁,锁就失去了互斥性

   2.redlock:

4. Redis 持久化机制，有几种方式，优缺点是什么，怎么实现的，RDB和AOF的区别

   RDB(redis database):直接保存数据库状态(键值对)的二进制文件

   ​	优点:1.rdb产生多个数据文件,适合做备份

   ​		2.rdb在持久化时是从redis进程fork出的子进程进行io处理不会影响主进程对外提供服务

   ​		3.rdb恢复数据时比aof快

   ​	缺点:1.rdb是定时生成数据文件,如果在一个时间段内没有生成数据文件就宕机则丢失了该时段是数据

   ​		2.fork子进程时如果文件过大会导致服务暂停一段时间

   AOF(appendonly file):保存服务器所执行的写命令来记录数据库状态

   ​	优点:1.aof一般会以每隔一秒去执行一次同步操作,所有如果redis进程宕掉最多失去1秒的数据

   ​		2.aof以append-only模式吸入,没有磁盘寻址开销,写入性能高

   ​		3.aof日志文件可读性强

   ​	缺点:1.对于同一份文件,aof比rdb数据快照要大

   ​		2.数据恢复慢

5. Redis集群，高可用，原理。

6. Redis的数据淘汰策略

   1. volatile-lru:从过期的数据集中选出最少使用的key
   2. allkeys-lru:从所有数据中选出最少使用的key
   3. volatile-random:从过期数据集中随机选出key
   4. allkeys-random:从所有数据集中随机选出key
   5. volatile-ttl:删除过期时间最短的key
   6. noenviction:不删除数据,报错

7. 为什么要用redis？为什么要用缓存，在哪些场景使用缓存

   热点数据的使用

8. redis事务，了解吗，了解Redis事务的CAS操作吗

   multi
   ...
   exec

   由multi命令开始将每个命令入队,然后使用exec一次执行

   redis事务的cas(乐观锁)由watch命令实现

   在执行命令之前使用watch加锁

   使用过后使用unwatch释放锁

9. 如何解决 Redis 的并发竞争Key问题。

   使用watch实现乐观锁,分布式锁setnx+expire实现,redlock

10. Redis为什么是单线程的，为什么单线程还这么快？

    redis基于内存,所以cpu不是redis的主要限制,主要限制是内存和网络带宽,故单线程

    1.单线程无需考虑各种锁的情况,没有锁的性能开销

    2.单线程多进程集群方案可代替多线程

    3.单线程没有上下文切换和竞争条件,不会消耗cpu,如果需要充分利用cpu可多开进程

    4.采用数据结构对数据存储进行优化

11. 如何保证缓存与数据库双写时的数据一致性?

    删除缓存而不是更新缓存?->懒加载思想

    缓存不一致问题:

    1.先修改数据库再删除缓存,删除缓存失败会出现读到旧数据,而数据库是最新的

    ​	解决:先删缓存再删数据库

    2.先删缓存,然后写数据库,此时还没写完成就查询数据库,查到修改前的旧数据放到缓存中

    ​	解决:可将读取到空缓存的请求放到队列中,写数据库成功后处理请求

12. redis和memcached有什么区别

    数据类型:redis有多中数据类型,而memcached只有k-v

    淘汰策略:redis会有过期策略,memcached不会主动定期检查需要淘汰数据,而是读取数据时检查时间戳或者当内存不够时需要主动淘汰数据时使用lru检查数据

    持久性:redis支持持久化存储,m不支持

    分布式:redis支持主从复制,m可使用一致性hash

    value:m是内存缓存,key小于250字符,单个item小于1M,不适合虚拟机使用

    数据一致性:redis使用单线程模型,存储大数据量比不过m,但保证了数据按顺序提交,m需要使用cas乐观锁来保证数据一致

13. JVM本地缓存，了解过吗

14. redis的list结构相关的操作。

    Hset,Hget,Hgetall

15. redis2和redis3的区别，redis3内部通讯机制。

16. Redis的选举算法和流程是怎样的？

17. Reids的主从复制机制原理。

18. Redis的线程模型是什么？

19. Redis的使用要注意什么，讲讲持久化方式，内存设置，集群的应用和优劣势，淘汰策略等。

20. Redis缓存分片

21. redis的集群怎么同步的数据的？

22. 请思考一个方案，设计一个可以控制缓存总体大小的自动适应的本地缓存。

23. redis的哨兵模式，一个key值如何在redis集群中找到存储在哪里。

24. Redis，一个字符串类型的值能存储最大容量是多少？

25. MySQL里有2000w数据，redis中只存20w的数据，如何保证redis中的数据都是热点数据？

    设置redis的淘汰策略为volatile-lru,会自动淘汰冷数据

26. Redis和Redisson有什么关系？

    redisson是redis的java客户端

27. Redis中的管道有什么用？

28. Redis事务相关的命令有哪几个？

    multi, exec, discard, watch, unwatch

29. Redis回收使用的是什么算法？

    lru最少使用算法

30. 一个Redis实例最多能存放多少的keys？List、Set、Sorted Set他们最多能存放多少元素？

31. Redis—跳跃表，复杂度是多少？

32. Redis有哪些优缺点？为什么要用 Redis ？

33. 为什么要用Redis 而不用 map/guava 做缓存?

    map/guava是内存缓存,只能在单体应用中使用,用于分布式需要更多自己实现的操作

34. 如何用 Redis 统计独立用户访问量？

    独立用户指唯一id

    1.使用唯一id作为key存set,查看set长度就可统计数量

    2.使用bitmap存储

    3.使用hyperloglog

35. 如何选择合适的持久化方式

    需要恢复速度快,占用内存少,丢失数据能接受较多则使用rdb

    能接受恢复速度,占用内存,丢失数据少则使用aof

36. Redis持久化数据和缓存怎么做扩容？

37. Redis key的过期时间和永久有效分别怎么设置？

    expire设置过期时间,不设置则为永久有效

38. 我们知道通过expire来设置key 的过期时间，那么对过期的数据怎么处理呢?

    服务器使用删除策略处理

39. Redis的过期键的删除策略

    定时删除:在设置过期时间就会设置一个定时器,时间到来就删除key,,浪费数据库资源

    惰性删除:放任key过期不管,当key被访问时才检查key是否过期,如果过期就删除键,浪费内存

    定期删除:每个一段时间扫描数据库,检查过期key删除

40. Redis的内存用完了会发生什么？

    redis使用默认的noenviction内存回收策略,内存用完再写入会报错

41. Redis如何做内存优化？

42. Redis事务的三个阶段

    multi 开始, 命令入队, exec 执行,discard 回滚

43. Redis事务相关命令

    mutil, exec, discard, watch, unwatch

44. Redis事务保证原子性吗，支持回滚吗？

    在命令队列中的命令要么全部执行要不全不执行,所以支持原子性

    不支持回滚,在遇到错误命令语句不会影响其他语句

45. Redis事务支持隔离性吗？

    支持,因为是单线程,事务总是串行执行且具有原子性,故支持隔离性

46. Redis集群的主从复制模型是怎样的？

    一主多从,master负责写,slave只能读

47. 生产环境中的 redis 是怎么部署的？

48. 说说Redis哈希槽的概念

49. Redis集群会有写操作丢失吗？为什么？

50. Redis集群最大节点个数是多少？

51. Redis集群如何选择数据库？

52. Redis是单线程的，如何提高多核CPU的利用率？

    开启多个进程,然后使用主从复制

53. 为什么要做Redis分区？有什么缺点？

54. 你知道有哪些Redis分区实现方案？

55. 缓存的实现原理，设计缓存要注意什么

56. 如何解决 Redis 的并发竞争 Key 问题

57. 分布式Redis是前期做还是后期规模上来了再做好？为什么？

58. 什么是 RedLock？

59. Redis支持的Java客户端都有哪些？官方推荐用哪个？

60. 为什么Redis的操作是原子性的，怎么保证原子性

61. Redis常见性能问题和解决方案？

62. 一个字符串类型的值能存储最大容量是多少？

63. Redis如何做大量数据插入？

64. 假如Redis里面有1亿个key，其中有10w个key是以某个固定的已知的前缀开头的，如果将它们全部找出来？

65. 使用Redis做过异步队列吗，是如何实现的？

66. Redis如何实现延时队列？

67. Redis回收进程如何工作的？

68. 热点数据和冷数据是什么

    在缓存中最频繁被访问的数据较热数据,反之就是冷数据

69. 使用过Redis哪些命令？

### 计算机网络

1. 请详细介绍一下TCP 的三次握手机制，为什么要三次握手？

   客户端发送含有syn的报文给服务端 --> 服务端确认自己能正常收到该客户端的消息

   服务端发送含有syn-ack的报文给客户端 --> 客户端确认自己能正常发送正常接收服务器消息,对方能正常发送正常接收消息

   客户端再次发送含有syn-ack的报文给服务端 --> 服务端确认自己能正常发送,接收客户端消息,客户端能正常发送,接收消息

2. 讲一下HTTP与HTTPS 的区别。

   https在tcp的基础之上增加一层ssl加密操作

3. Session和cookie的区别。

   session存储在服务器通过session_id取,cookie存储在浏览器

   cookie只能存储ASCII码,session则能存储任何数据类型

4. TCP的四次挥手，为什么要有TIME_WAIT 状态，为什么需要四次握手

   客户端发送含有fin的报文给服务端 

   服务端收到后发出确认,此时处于半关闭状态,服务端能发数据给客户端,客户端不能发服务端

   服务端发出连接释放报文,fin

   客户端收到后发出确认,进入TIME-WAIT状态等待2MSL(最大报文存活时间)后释放连接

   服务端收到客户端的确认后释放连接

   四次挥手原因

   ​	客户端发送FIN报文请求释放连接后,服务器收到报文后,就进入CLOSE-WAIT状态,这个状态是为了让服务器发送还未传送完毕的数据,传送完毕之后,服务器会发送FIN连接释放报文

   使用TIME_WAIT理由:

   ​	确保服务端收到最后一个确认报文,如果服务端没有收到确认报文就会重新发送连接释放请求

   ​	让本连接持续时间所产生的报文在网络中小时,等到下一个连接时不会有旧的请求报文

5. http1.0和http1.1有什么区别。

6. HTTP的常见状态码有哪些，代表什么含义？比如200, 302, 404？

7. 当你用浏览器打开一个链接到返回结果，发生了什么。

   浏览器拿到连接去DNS请求IP地址,拿到IP地址建立HTTP连接,向web服务器发送http请求,web服务器处理请求返回页面,浏览器解析页面

8. TCP/IP如何保证可靠性，说说TCP头的结构。

9. GET与POST方式的区别

10. 如何避免浏览器缓存。

11. TCP/IP模型?

12. 讲一讲 TCP 和 UDP 各有什么特点，两者有什么区别

13. 详细讲一下TCP的滑动窗口

14. 说一下拥塞控制

15. 如何理解HTTP协议的无状态性。

16. HTTP有哪些 method？

17. HTTP长连接和短连接

18. HTTPS原理，加签，验签，什么是数字签名？什么是数字证书？对称加密和非对称加密等。

19. 谈下你对 IP 地址分类的理解？

20. ARP及RARP协议的工作原理？

21. 怎么解决拆包和粘包？

22. DNS 的解析过程？

23. 什么是DoS、DDoS、DRDoS攻击？如何防御？

24. WebSocket与socket的区别

25. 讲一讲SYN超时，洪泛攻击，以及解决策略

26. ICMP协议的功能

27. 什么是 session，有哪些实现 session 的机制？

28. Http请求的过程与原理

29. 你知道网络协议有那些？

30. HTTPS 为什么是安全的？说一下他的底层实现原理？

31. ping的原理

32. 如果服务器出现了大量 CLOSE_WAIT 状态如何解决。

33. TCP 黏包是怎么产生的？

34. OSI七层体系结构路

35. 由器与交换机的区别

36. 什么是XSS攻击，如何避免

37. 什么是CSRF攻击，如何避免

38. Https双向和单向验证的区别

39. 如果客户端禁止Cookie能实现Session

40. HTTP请求中session实现原理

### 消息队列

1. 消息队列有哪些使用场景。
2. 消息中间件如何解决消息丢失问题？
3. 谈谈消息的重发，补充策略。
4. 如何保证消息的顺序性。
5. 怎么利用mq实现最终一致性？
6. kafka 和其他消息队列的区别，kafka 主从同步怎么实现？
7. MQ的连接是线程安全的吗，你们公司的MQ服务架构怎样的。
8. kafka吞吐量高的原因。
9. rabbitmq如何实现集群高可用？
10. 使用kafka有没有遇到什么问题，怎么解决的？
11. MQ有可能发生重复消费，如何避免，如何做到幂等？
12. MQ的消息延迟了怎么处理，消息可以设置过期时间么，过期了你们一般怎么处理？
13. rabbitmq 有几种广播类型？
14. 使用 kafka 集群需要注意什么？
15. 为什么使用消息队列？有什么用？
16. 消息队列有什么优点和缺点？
17. Kafka、ActiveMQ、RabbitMQ、RocketMQ 都有什么区别，以及适合哪些场景？
18. MQ能否保证消息必达，即消息的可靠性
19. 大量消息在MQ里长时间积压，该如何解决？
20. MQ消息过期失效怎么办？
21. kafka可以脱离zookeeper单独使用吗？为什么？
22. kafka 的分区策略有哪些？
23. kafka 有几种数据保留策略？
24. RabbitMQ 中的 broker 是指什么？cluster 又是指什么？
25. Kafka 消息是采用 Pull 模式，还是 Push 模式？
26. RabbitMQ 有哪些重要组件
27. 如何确保消息接收方消费了消息？
28. 消息基于什么传输？
29. 消息怎么路由？
30. 消息如何分发？

### mybatis

1. mybatis 中 #{}和 ${}的区别是什么？

   #{}:mybatis将#{}替换为?,将sql预编译用preparedStatement.set注入参数,防止sql注入

   ${}:直接将参数和${}替换,mybatis不做处理

2. 什么是SQL注入 ，如何避免。

   sql注入:在非预想情况下传入拼接字符串使得sql语句操作预想之外的结果,在mybatis中通常使用${}会出现

   例如:select * from t where id = ${} ,传入值为"2 and name='wx'",这时候最终运行的sql语句为:select * from t where id = 2 and name='wx'

   使用#{}填充参数

3. 说一下 mybatis 的一级缓存和二级缓存

   一级缓存就是在sqlSession下的Executor中的LocalCache是简单k-v集合,每次查询判断语句是否已经查过然后直接返回缓存中的数据

   二级缓存属于namespace级别,多个SQLSession之间可以共享数据,使用CacheExecutor装饰Executor

4. mybatis 是否支持延迟加载？延迟加载的原理是什么？

5. mybatis 动态sql中使用标签与直接写where关键字有什么区别？

   where标签可以保证当标签块中没有语句时不会生成where语句

6. mybatis 动态sql标签中循环标签中有哪些属性，各自的作用。

   collection:读入的数据列表

   item:每个元素的命名

   index:元素位置

   open:遍历开始填充符

   close:截止填充符

   separator:分隔符

7. mybatis 和 hibernate 的区别有哪些？

8. RowBounds是一次性查询全部结果吗？为什么？

   是,RowBoundS分页实现的是逻辑分页,把全部符合条件的结果查出来,然后再取分页数据

9. MyBatis 定义的接口，怎么找到实现的？

   Mapper接口注册在SQLSessionFactory类的HashMap中,k为class,v为创建当前mapper的工厂

   Mapper注册只有从SQLSession中获取

   SQLSession.getMapper运用了动态代理,产生目标Mapper接口的代理对象

   动态代理完成增删改查方法的调用

10. Mybatis的底层实现原理。

    同上

11. Mybatis是如何进行分页的？分页插件的原理是什么？

    逻辑分页和物理分页,逻辑分页使用查询全部符合查询条件的数据,然后分页,物理分页使用limit

12. Mybatis执行批量插入，能返回数据库主键列表吗？

    能

13. Mybatis都有哪些Executor执行器？它们之间的区别是什么？

14. Mybatis动态sql有什么用？执行原理？有哪些动态sql？

15. mybatis有几种分页方式？

16. MyBatis框架的优点和缺点

17. 使用MyBatis框架，当实体类中的属性名和表中的字段名不一样 ，怎么办 ？

    使用别名或者resultMap

18. 通常一个Xml映射文件，都会写一个Dao接口与之对应，请问，这个Dao接口的工作原理是什么？Dao接口里的方法，参数不同时，方法能重载吗？

19. Xml映射文件中，除了常见的select|insert|updae|delete标签之外，还有哪些标签？

    <set>,<foreach>,<where><trim>,<if>

20. 简述Mybatis的插件运行原理，以及如何编写一个插件。

### 操作系统

1. Linux系统下你关注过哪些内核参数，说说你知道的。
2. epoll和poll有什么区别。
3. 线上CPU爆高，请问你如何找到问题所在。
4. Linux下IO模型有几种，各自的含义是什么。
5. top 命令之后有哪些内容，有什么作用。
6. 进程通信有几种方式？
7. 说说进程的调度算法
8. 常见的几种内存管理机制
9. 什么是虚拟内存(Virtual Memory)?
10. 内存置换算法
11. 虚拟地址、逻辑地址、线性地址、物理地址的区别。
12. 操作系统的页式存储
13. 进程和线程的区别
14. socket客户端和服务端通信过程
15. 影响调度程序的指标是什么？
16. 进程间状态有哪些？
17. 一个线程在内存中如何存储？
18. 僵尸进程是什么，如果产生一个僵尸进程，如何查找僵尸进程
19. 一个进程有20个线程，在某个线程中调用fork，新的进程会有20个线程吗？
20. 什么是 RR 调度算法？
21. 什么是 DMA（直接内存访问）？

### Spring 相关

1. BeanFactory和 ApplicationContext有什么区别？

   BeanFactory定义了一些对bean的基本操作,如getBean,containsBean()等等方法

   BeanFactory采用的是懒加载,只有当bean需要被使用的时候才使用getBean加载实例化

   ApplicationContext是BeanFactory的派生类,并支持更多的操作:

   ​	继承MessageSource可进行国际化

   ​	继承ApplicationEventPublisher实现事件机制

   ​	继承ResourceLoader可实现对底层资源的访问

   ​	ApplicationContext一开始就加载所有的bean

2. Spring IOC 的理解，其初始化过程

   IOC即控制反转:将原本需要程序代码直接操作对象的调用交给容器,容器负责创建对象,管理对象,装配对象,配置对象并且管理这些对象的整个生命周期

3. Spring Bean 的生命周期

   ![img](https://img-blog.csdnimg.cn/201911012343410.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoaW5rV29u,size_16,color_FFFFFF,t_70)

4. Spring MVC 的工作原理？

   前端发送请求到dispatcherServlet -> dispatcherServlet解析并找到匹配的handlerMapping -> 然后由despatcherServlet选择handlerAdapter处理 -> dispatcherServlet将处理结果传给ViewResolver解析 -> 解析数据返回渲染

5. Spring 循环注入的原理？

   ![1590732195478](C:\Users\duia\AppData\Roaming\Typora\typora-user-images\1590732195478.png)

6. Spring 中用到了那些设计模式？

   工厂模式,单例模式,观察者模式,代理模式,模板方法模式

7. Spring AOP的理解，各个术语，他们是怎么相互工作的？

   面向切面编程使用动态代理的方式,在不影响原有代码基础加强功能,比如日志记录每个方法的执行时间

   Spring AOP和ASpectJ AOP:

   ​	前者是动态代理,不会修改原代码,会在每次运行时在内存临时为方法生成一个动态代理类AOP对象,该对象包含了目标方法和增强处理

   ​	后者在编译阶段会生成代理类,然后将代码织入到字节码中,运行的时候就是增强之后的代理类即AOP对象

   JDK动态代理和CGLIB动态代理:

   ​	JDK动态代理,需要目标类继承InvocationHandler通过invoke()方法调用代码

   ​	CGLIB动态代理:无需类继承,可在运行时动态生成一个目标类的子类,并覆盖其中代码增加增强代码,目标类不能被final修饰否则无法被继承

8. Spring框架中的单例bean是线程安全的吗?

   不是,spring没有对bean做多线程处理,最简单的方法是单例bean设置为prototype,每次会创建一个新的bean

9. Spring @ Resource和Autowired有什么区别？

   @Resource是java自带的注解,默认byName

   @Autowired是Spring的注解,默认ByType,配置@Qualifier实现ByName查找bean

10. Spring 的不同事务传播行为有哪些，有什么作用？

    propagation_required:如果当前有事务就加入,没有事务就创建事务

    propagation_requires_new:每次创建新事物

    propagation_supports:支持当前事务,有事务就加入,没有事务就以非事务进行

    propagation_not_supports:以非事务运行,若当前有事务则挂起

    propagation_mandatory:支持当前事务,有事务就加入,没有事务就抛异常

    propagation_never:以非事务运行,有事务就抛异常

    propagation_nested:如果有事务就在嵌套事务内执行,没有则按照required进行

11. Spring Bean 的加载过程是怎样的？

12. 请举例说明@Qualifier注解

    配置@Autowired使用,当bean多个实现时需要使用@Qualifer配置指定注入bean

13. Spring 是如何管理事务的，事务管理机制？

    编程式,将事务代码写在业务代码中执行事务

    申明式,使用注解或者xml配置,实现业务代码和事务代码分离

14. 使用Spring框架的好处是什么？

15. Spring由哪些模块组成？

    spring-core,spring-beans,spring-context,spring-jdbc,spring-web,spring-test,spring-aop

16. ApplicationContext通常的实现是什么？

    FileSystemApplication:从全路径名中加载XML文件读取配置和加载bean

    ClassPathApplication:从classpath中加载XML文件读取配置和加载bean

    WebXmlApplication:从XMl文件中加载一个web应用的所有bean

17. 什么是Spring的依赖注入？

    DI:由容器以某种依赖关系将目标对象注入到组件对象中

18. 你怎样定义类的作用域？

    single,prototype,request,session,global session,

19. Spring框架中的单例bean是线程安全的吗？

    不是,spring没有对单例bean做多线程,需要自己维护或者将单例bean改为prototype每次创建新对象

20. 你可以在Spring中注入一个null 和一个空字符串吗？

    可以

21. 你能说下 Spring Boot 与 Spring 的区别吗

    spring boot是spring的脚手架,让开发者避免spring繁琐的配置

22. SpringBoot 的自动配置是怎么做的？

    Springboot中最重要的@SpringBootApplication包括三个注解:

    ​	@SpringBootConfiguration:整合@Configuration注解实现配置文件的功能

    ​	@EnableAutoConfiguration:开启自动配置

    ​	@ComponentScan:扫描组件

    其中@EnableAutoConfiguration的关键功能由AutoConfigurationImportSelector#selectImports提供:

    找到META-INFO下的spring.factories中的所有配置类

23. @RequestMapping 的作用是什么？

    设置http的请求url和请求方法,在类上不能设置请求方法

24. spring boot 有哪些方式可以实现热部署？

    加devtools插件,然后加springboot-maven插件中的fork属性设为true

    idea上jrebel插件

25. 说说Ioc容器的加载过程

    资源定位:读取配置文件

    解析资源

    注册bean

    实例化:BeanFactory的getBean

26. 为什么 Spring 中的 bean 默认为单例？

    因为只有单例bean才会在容器中被管理,如果是prototype每生成新的bean就不会被容器管理

27. 说说Spring中的@Configuration

    标志该类是一个配置类,spring会去该类下读取以@Bean修饰的方法注册bean被容器管理

28. FileSystemResource 和ClassPathResource 有何区别？

    FileSystemResource和ClassPathResource和ServletContextResource都是获取资源的类

    FileSystemResource在File类的基础上做的封装

    ClassPathResource是在系统类路径中加载

29. 什么是 Swagger？你用 Spring Boot 实现了它吗？

    Rest API文档生成工具

30. spring的controller是单例还是多例，怎么保证并发的安全。

    默认单例

    并发安全本质是处理共享变量:

    ​	将单例设置为prototype原型,每次生成新对象

    ​	使用Threadlocal装载数据变量

    ​	加锁

31. 说一下Spring的核心模块

32. 如何向 Spring Bean 中注入一个 Java.util.Properties

    在xml文件中在bean标签下配置prop标签

33. 如何给Spring 容器提供配置元数据?

    用xml配置文件配置bean

    用注解如@Controller,需要开启component-scan

    用java-config使用@Configuration下@Bean

34. 如何在Spring中如何注入一个java集合，实现过吗？

    在property标签下配置list,set,map标签使用

35. 什么是基于Java的Spring注解配置? 举几个例子？

    基于@Configuration和@Bean

36. 怎样开启注解装配？

    配置context:annotation-config标签

37. Spring支持哪些事务管理类型

    声明式:使用注解@Transaction

    编程式:手动编写事务代码

38. 在Spring AOP 中，关注点和横切关注的区别是什么？

    关注点是具体业务关注点,横切是关注整个应用,整个应用都会使用的功能如日志

39. spring 中有多少种IOC 容器？

    BeanFactory和ApplicationContext

40. 描述一下 DispatcherServlet 的工作流程

    前端发送http请求被DispatcherServlet捕获

    dispatcherServlet解析url得到uri然后用uri去配对handlerMapping获取handler

    然后用handler选择handlerAdapter处理调用处理器返回modelAndView给dispatcherServlet

    dispatcherServlet转发给视图解析器ViewResolver渲染

    将渲染结果返回给前端显示

    ![img](https://imgedu.lagou.com/5587746310b14c138bae8fd50b2c8f71.jpg)

41. 介绍一下 WebApplicationContext吧

    WebApplicationContext继承自ApplicationContext,额外提供关于WebServlet关联的能力

42. Spring Boot 的配置文件有哪几种格式？它们有什么区别？

    properties和yml,yml层次性强,可读性强

43. Spring Boot 需要独立的容器运行吗？

    不需要,内置了Tomcat和jetty

44. Spring Boot 自动配置原理是什么？

    @EnableConfiguration,@Configuration和@ConditionOnClass是自动装配的核心

    @EnableConfiguration上导入了继承importSelector类的子类,其中的selectImports会去配置文件读取自动配置器,然后自动配置器注册装配bean

45. RequestMapping 和 GetMapping 的不同之处在哪里？

    @GetMapping相当于@RequestMapping(method="get")

46. 如何使用Spring Boot实现异常处理？

    使用@ControllerAdvice可以全局抓异常

47. Spring Boot 中如何解决跨域问题 ?

    前端使用jsonp

    后台使用@CrossOrigin

48. Spring Boot 如何实现热部署 ?

    使用devtools插件或者idea的jrebel插件

49. Spring Boot打成的 jar 和普通的jar有什么区别呢?

    springboot的jar包选择生成默认jar包和可依赖jar包,默认jar包层次不同不可被依赖

50. bootstrap.properties 和 application.properties 有何区别 ?

    前者优先于后者被加载

51. springboot启动机制

### Netty/tomcat

1. BIO、NIO和AIO区别
2. 说一下Netty 的各大组件
3. Netty 线程模型和 Reactor 模式
4. 什么是 Netty 的零拷贝？
5. NIO 的底层实现。
6. netty的心跳处理在弱网下怎么办
7. Netty 高性能表现在哪些方面？
8. Netty 和 Tomcat 有什么区别？
9. Netty 发送消息有几种方式？
10. 默认情况 Netty 起多少线程？何时启动？
11. Netty 支持哪些心跳类型设置？
12. Java 中怎么创建 ByteBuffer
13. Java 中的内存映射缓存区是什么？
14. 简单讲讲tomcat结构，以及其类加载器流程，线程模型等
15. tomcat如何调优，涉及哪些参数
16. IO多路复用机制
17. Netty 的应用场景有哪些？
18. 有几种I/O 网络模型？
19. 说说Netty的执行流程？
20. select、poll、epoll的机制及其区别？

### 常用Linux 命令

1. 修改目录，文件权限的命令
2. 如何获取一个本地服务器上可用的端口。
3. 说说常见的linux命令，linux查看内存的命令是什么？
4. 查看系统磁盘空间剩余情况的命令
5. 如何获取java进程的pid
6. 如何获取某个进程的网络端口号；
7. 如何实时打印日志
8. 如何统计某个字符串行数；
9. 用一行命令查看文件的最后五行。
10. 用一行命令输出正在运行的java进程。
11. 绝对路径，当前目录、上层目录，切换目录分别用什么命令？
12. 怎么清屏？怎么退出当前命令？
13. 目录创建，创建文件，复制文件分别用什么命令？
14. 查看文件内容有哪些命令可以使用？tail？cat？less？more？
15. 怎么使一个命令在后台运行?
16. 终止进程用什么命令? 带什么参数? kill-9 pid有什么风险？
17. 搜索文件用什么命令? 格式是怎么样的?
18. 使用什么命令查看网络是否连通?
19. 使用什么命令查看 ip 地址及接口信息？
20. awk 详解

### ZooKeeper

1. Zookeeper的用途，选举的原理是什么。
2. Zookeeper watch机制原理。
3. zookeeper 怎么保证主从节点的状态同步？
4. 集群中有3台服务器，其中一个节点宕机，这个时候 zookeeper 还可以使用吗？
5. zookeeper都有哪些功能？
6. 什么是paxos算法，什么是zab协议。
7. zookeeper 是如何保证事务的顺序一致性的？
8. zookeeper 负载均衡和 nginx 负载均衡区别
9. Zookeeper 的典型应用场景
10. 说说四种类型的数据节点Znode
11. Zookeeper 的服务器角色（Leader，Follower，Observer）
12. Zookeeper 有哪几种几种部署模式？

### Elasticsearch

1. 详细描述一下Elasticsearch索引文档的过程。
2. 详细描述一下Elasticsearch搜索的过程。
3. Elasticsearch 的倒排索引是什么。
4. Elasticsearch是如何实现master选举的。
5. lucence内部结构是什么。
6. Lucene全文搜索的原理
7. 在并发情况下，Elasticsearch 如何保证读写一致呢？
8. 详细阐述一下 Elasticsearch 搜索的过程。
9. Elasticsearch 索引数据多了怎么办呢，如何调优，部署
10. Elasticsearch 对于大数据量（上亿量级）的聚合如何实现？

### dubbo框架

1. Dubbo的服务请求失败怎么处理
2. dubbo的负载均衡有几种算法?（随机，轮询，最少活跃请求数，一致性hash）
3. Dubbo 和 Spring Cloud 有什么区别？
4. dubbo都支持什么协议，推荐用哪种？
5. 画一画服务注册与发现的流程图
6. Dubbo默认使用什么注册中心，还有别的选择吗？
7. 在 Provider 上可以配置的 Consumer 端的属性有哪些？
8. Dubbo启动时如果依赖的服务不可用会怎样？
9. Dubbo推荐使用什么序列化框架，你知道的还有哪些？
10. Dubbo默认使用的是什么通信框架，还有别的选择吗？
11. 服务上线怎么兼容旧版本？
12. Dubbo服务之间的调用是阻塞的吗？
13. Dubbo telnet 命令能做什么？
14. Dubbo如何一条链接并发多个调用。
15. Dubbo 的使用场景有哪些？
16. Dubbo 核心功能有哪些？
17. Dubbo 核心组件有哪些？
18. Dubbo 服务器注册于发现的流程？
19. Dubbo 支持哪些协议，它们的优缺点有哪些？
20. Dubbo 的注册中心集群挂掉，发布者和订阅者之间还能通信么？
21. Dubbo源码使用了哪些设计模式
22. Dubbo集群提供了哪些负载均衡策略？
23. Dubbo的集群容错方案有哪些？
24. Dubbo 支持哪些序列化方式？
25. Dubbo超时重试，Dubbo超时时间设置

### spring cloud

1. Eureka和Zookeeper区别
2. 什么是服务熔断？什么是服务降级?
3. 什么是Ribbon？
4. 什么是 Netflix Feign？它的优点是什么？
5. Ribbon和Feign的区别？
6. 什么是Spring Cloud Bus?
7. Spring Cloud Gateway?
8. 什么是SpringCloudConfig?
9. 什么是 Hystrix？它如何实现容错？
10. 什么是微服务？微服务优缺点
11. Sentinel，微服务哨兵，了解过吗

### nginx

1. Nginx的模块与工作原理是什么?
2. Nginx 是什么？有什么作用？
3. 说说Nginx的一些特性。
4. 请说一下Nginx如何处理HTTP请求。
5. 你知道，Nginx服务器上的Master和Worker进程分别是什么吗?
6. nginx常用命令，启动，重启，检查配置文件等
7. Nginx 和 Apache 比较，各有什么优缺点?
8. Nginx 多进程模型是如何实现高并发的？
9. 说说Nginx的反向代理和负载均衡
10. 请列举Nginx服务器的最佳用途。

### 算法

1. 谈一谈一致性哈希算法。

2. 快排怎么实现

3. 手写二分查找

4. 如何判断一个单链表是否有环

5. 平衡二叉树的时间复杂度；

6. 反转单链表

7. 合并多个单有序链表

8. LRU 淘汰算法，用java自己实现一个LRU。

   lru:最少使用算法

   可使用LinkedHashMap实现

   设置最大容量,重写removeEldestEntry方法,删除条件为实际容量大于设置容量

   使用LinkedHashMap构造参数,设置accessOrder开启lru顺序

9. 跳表和平衡树区别

10. 你了解大O符号(big-O notation)么？你能给出不同数据结构的例子么？

11. 如何手撸一个队列？

12. 10亿个数字里里面找最小的10个。

13. 平衡二叉树的时间复杂度；

14. 有1亿个数字，其中有2个是重复的，快速找到它，时间和空间要最优。

15. 八大基本排序的时间，空间复杂度

16. 堆排序的原理

17. 树的几种遍历方式

18. 递归算法

19. 一个乱序数组，求第K大的数。排序方式使用字典序。

20. 一棵二叉树，求最大通路长度。

21. 万亿级别的两个URL文件A和B，如何求出A和B的差集C,(Bit映射->hash分组->多文件读写效率->磁盘寻址以及应用层面对寻址的优化)

22. 最快的排序算法是哪个？给阿里2万多名员工按年龄排序应该选择哪个算法？堆和树的区别；写出快排代码；链表逆序代码

23. LeetCode的经典算法题目，都要刷一遍以上哈~

### 分布式

1. 说说分布式事务？分布式事务的解决方案
2. 什么是分布式系统？
3. 讲讲CAP理念。
4. 怎么理解强一致性、单调一致性和最终一致性？
5. 如何实现分布式锁？
6. 如何实现分布式 Session?
7. 负载均衡的理解？
8. 分布式集群下如何做到唯一序列号？
9. 分布式事务
10. 什么是一致性hash。

### 系统设计/方案设计

1. 谈谈如何设计秒杀系统。
2. 一千万的用户实时排名如何实现；
3. 五万人并发抢票怎么实现
4. 手机扫二维码登录是怎么实现的？
5. Google是如何在一秒内把搜索结果返回给用户的。
6. 12306网站的订票系统如何实现，如何保证不会票不被超卖。
7. 如果有几十亿的白名单，每天白天需要高并发查询，晚上需要更新一次，如何设计这个功能。
8. 接口的幂等性如何设计
9. 如何设计存储海量数据的存储系统
10. 分布式session如何管理，你有哪些方案
11. 讲一下如何给高并发系统做限流？
12. 使用SpringBoot如何开发邮件发送系统？
13. 你如何设计一个能抗住大流量的系统，说说设计方案
14. 如何设计一个高并发的系统？
15. 数据量大的情况下分页查询很慢，有什么优化方案？
16. 设计一个秒杀系统，30分钟没付款就自动关闭交易。
17. 如何使用redis和zookeeper实现分布式锁？有什么区别优缺点，会有什么问题，分别适用什么
18. 如何设计一个安全的API接口。
19. 线上系统突然变得异常缓慢，你如何查找问题。
20. 设计一个社交网站中的“私信”功能，要求高并发、可扩展等等。画一下架构图。
21. 后台系统怎么防止请求重复提交
22. 讲讲你理解的服务治理。
23. 执行某操作，前50次成功，第51次失败a全部回滚b前50次提交第51次抛异常，ab场景分别如何设置
24. 一个大的含有50M个URL的记录，一个小的含有500个URL的记录，找出两个记录里相同的URL
25. 海量日志数据，提取出某日访问百度次数最多的那个IP
26. 1000个线程同时运行，怎么防止不卡
27. 设计一个分布式自增id生成服务
