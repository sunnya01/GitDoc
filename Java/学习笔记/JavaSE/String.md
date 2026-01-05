##### String

###### 常用类

字符串相关: String StringBuffer StringBuilder

日期相关: System Date Calendar SimpleDateFormat LocalDate LocalTime LocalDateTime Instand DateTimeFormatter

比较器: Comparable Comparator

System类、Math类、BigInteger与BigDecimal类

###### String类内存分析

如果是通过String str = "abc" 字面量的赋值形式，本质现在方法区的常量池新建一个单字符数组，并将对象

str地址值指向该地址

如果是String str = new String("abc")新建对象的形式，本质str对象先指向一个堆空间的地址值，堆空间中的value再指向一个方法区常量池里面的单字符数组

注意: 任何字符串的调整都会在方法区常量池中开辟新的单字符数组。并更改上述的地址指向值(str = str + "b"字符串如果只有字面量进行拼接则不创建堆空间对象，否则将跟new String("")类似先创建堆空间再在堆空间中的String对象的value属性赋值char[]数组的首地址)

例：String s1 = "abc"; String s2 = "abc";由于都是字面量的形式创建了字符串对象，因此他们都不经过堆空间，对象的地址值直接指向的是方法区常量池的单字符数组首地址值。String s3 = new String("def"); String s4 = new String("def");虽然方法区常量池中他们指向了同一个数组但是由于开辟的堆空间中是两个独立的对象因此他们s3 == s4 为false，但是他们内部value的地址值是相同的