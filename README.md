####1.java 语言如何进行异常处理，关键字：throws、throw、try、catch、finally分别代表什么意义？finally代码是在return之后还是之前执行？

throws是获取异常，throw是抛出异常，try是将会发生异常的语句括起来，从而进行异常的处理，
catch是如果有异常就会执行他里面的语句，而finally不论是否有异常都会进行执行的语句。
两种情况下finally语句是不会被执行的：
（1）try语句没有被执行到，如在try语句之前就返回了，这样finally语句就不会执行，这也说明了finally语句被执行的必要而非充分条件是：相应的try语句一定被执行到。

（2）在try块中有System.exit(0);这样的语句，System.exit(0);是终止Java虚拟机JVM的，连JVM都停止了，所有都结束了，当然finally语句也不会被执行到。

####2.一只蜗牛掉进10米深的井中。白天往上爬4米晚上又掉下去3米。请问要几天才能爬出来井口?
 7天。 计算: 6*(4-3)+4=10
####3.abstract class和interface有什么区别?接口可以继承接口吗？接口可以继承抽象类吗，为什么？
1.抽象类可以有构造方法，接口中不能有构造方法。
2.抽象类中可以有普通成员变量，接口中没有普通成员变量
3.抽象类中可以包含非抽象的普通方法，接口中的所有方法必须都是抽象的，不能有非抽象的普通方法。
4. 抽象类中的抽象方法的访问类型可以是public，protected和（默认类型,虽然
eclipse下不报错，但应该也不行），但接口中的抽象方法只能是public类型的，并且默认即为public abstract类型。
5. 抽象类中可以包含静态方法，接口中不能包含静态方法
6. 抽象类和接口中都可以包含静态成员变量，抽象类中的静态成员变量的访问类型可以任意，但接口中定义的变量只能是public static final类型，并且默认即为public static final类型。
7. 一个类可以实现多个接口，但只能继承一个抽象类。
接口可以继承(extends)接口,但是抽象类不能继承接口,可以通过implements去实现接口，抽象类是可以继承实体类。
抽象类不能通过new的方式创建出来，只能通过extends继承实现。
在实现抽象类时，必须实现该类中的每一个抽象方法，而每个已实现的方法必须和抽象类中指定的方法一样，接收相同数目和类型的参数，具有同样的返回值。
####4.SQL Select语句完整的执行顺序： 
1、from子句组装来自不同数据源的数据；
2、where子句基于指定的条件对记录行进行筛选；
3、group by子句将数据划分为多个分组；
4、使用聚集函数进行计算；
5、使用having子句筛选分组；
6、计算所有的表达式；
7、select 的字段；
8、使用order by对结果集进行排序。
####5.请说出单例模式的优缺点，并判断下面代码可能会出现的问题并提出你的解决方案（代码方式）
 1.public static Singleton getInstance(){
     if(instance == null){
        instance = new Singleton();
     }
     return instance;
   }
主要优点：
1、提供了对唯一实例的受控访问。
2、由于在系统内存中只存在一个对象，因此可以节约系统资源，对于一些需要频繁创建和销毁的对象单例模式无疑可以提高系统的性能。
3、允许可变数目的实例。
主要缺点：
1、由于单利模式中没有抽象层，因此单例类的扩展有很大的困难。
2、单例类的职责过重，在一定程度上违背了“单一职责原则”。
3、滥用单例将带来一些负面问题，如为了节省资源将数据库连接池对象设计为的单例类，可能会导致共享连接池对象的程序过多而出现连接池溢出；如果实例化的对象长时间不被利用，系统会认为是垃圾而被回收，这将导致对象状态的丢失。
可能会出现的问题:多个线程判断instance都为null时，在执行new操作时多线程会出现重复情况
解决方案：加锁synchornized
public static  synchornized Singleton getInstance(){
     if(instance == null){
        instance = new Singleton();
     }
     return instance;
   }
优点 资源利用率高，不执行getInstance()就不会被实例，可以执行该类的其他静态方法 
缺点 第一次加载时不够快，多线程使用不必要的同步开销大 
####6.请简述MVC的含义，并说明MVC处理的原理和哪些技术来实现。
MVC是Model－View－Controller的简写。Model 代表的是应用的业务逻辑（通过JavaBean，EJB组件实现）， View 是应用的表示面（由JSP页面产生），Controller 是提供应用的处理过程控制（一般是一个Servlet），通过这种设计模型把应用逻辑，处理过程和显示逻辑分成不同的组件实现。这些组件可以进行交互和重用。
####7.请说明AJAX异步刷新原理和XmlHttpRequest的基本属性，并说明AJAX在提交请求后readyState返回值为3和4代表含义。
XmlHttpRequest使您可以使用JavaScript向服务器提出请求并处理响应，而不阻塞用户。
readyState
对象状态值：
* 0 = 未初始化（uninitialized）
* 1 = 正在加载（loading）
* 2 = 加载完毕（loaded）
* 3 = 交互（interactive）
* 4 = 完成（complete）
####8.Hibernate中Inverse和Cascade的区别
作用的范围不同： 
     Inverse是设置在集合元素中的。 
    Cascade对于所有涉及到关联的元素都有效。 
    <many-to-one/><ont-to-many/>没有inverse属性，但有cascade属性 
执行的策略不同 
    Inverse 会首先判断集合的变化情况，然后针对变化执行相应的处理。 
    Cascade 是直接对集合中每个元素执行相应的处理 
执行的时机不同 
     Inverse是在执行SQL语句之前判断是否要执行该SQL语句 
     Cascade则在主控方发生操作时用来判断是否要进行级联操作 
执行的目标不同 
     Inverse对于<ont-to-many>和<many-to-many>处理方式不相同。 
   对于<ont-to-many>，inverse所处理的是对被关联表进行修改操作。 
   对于<many-to-many>，inverse所处理的则是中间关联表 
     Cascade不会区分这两种关系的差别，所做的操作都是针对被关联的对象。 

总结： 
<one-to-many>中，建议inverse=”true”，由“many”方来进行关联关系的维护 
<many-to-many>中，只设置其中一方inverse=”false”，或双方都不设置 
Cascade，通常情况下都不会使用。特别是删除，一定要慎重。 
####9.用一条SQL语句 查询出每门课都大于80分的学生姓名 
name   kecheng   fenshu 
张三     语文       81
张三     数学       75
李四     语文       76
李四     数学       90
王五     语文       81
王五     数学       100
select Name from student where fenshu>80 group by Name having COUNT(*)>1
####10.有两个表A 和B ，均有key 和value 两个字段，如果B 的key 在A 中也有，就把B 的value 换为A 中对应的value
update B b set a.value=(select value from A a  where  b.key = a.key)  where exist (select 1 from A c where c.key = b.key)
 
####11.请用sql语句写出ORACLE数据库user表分页，每页10条记录。
select * from (select rownum rm,t.* from (select * from user)t where rownum <= 10) where rm > 1
####12.Hibernate中悲观锁和乐观锁
Hibernate悲观锁：在数据有加载的时候就给其进行加锁，直到该锁被释放掉，其他用户才可以进行修改，优点：数据的一致性保持得很好，缺点：不适合多个用户并发访问。当一个锁住的资源不被释放掉的时候，这个资源永远不会被其他用户进行修改，容易造成无限期的等待。
Hibernate乐观锁：就是在对数据进行修改的时候，对数据才去版本或者时间戳等方式来比较，数据是否一致性来实现加锁。优点比较好。
####13.Hibernate三种状态的概念
Hibernate三种状态之一：临时状态（Transient）：用new创建的对象，它没有持久化，没有处于Session中，处于此状态的对象叫临时对象；
Hibernate三种状态之二：持久化状态（Persistent）：已经持久化，加入到了Session缓存中。如通过hibernate语句保存的对象。处于此状态的对象叫持久对象；
Hibernate三种状态之三：游离状态（Detached）：持久化对象脱离了Session的对象。如Session缓存被清空的对象。特点：已经持久化，但不在Session缓存中。处于此状态的对象叫游离对象；
####14.Hibernate get和load区别
1.get()采用立即加载方式,而load()采用延迟加载;
  get()方法执行的时候,会立即向数据库发出查询语句,
  而load()方法返回的是一个代理(此代理中只有一个id属性),只有等真正使用该对象属性的时候,才会发出sql语句
2.如果数据库中没有对应的记录,get()方法返回的是null.而load()方法出现异常ObjectNotFoundException


#### 面试另外一个家伙：

我：你能描述一下你最近开发的项目、以及使用到的技术吗？

应试者： 那是个XYZ系统，我们使用了Spring，Hibernate，REST WebServices。

我：那好。你能解释一下RESTful吗？

应试者：我们使用@RequestMapping(value=”/url”, method=”POST”)来开发RESTful应用。我们还使用了PUT，DELETE方法。

我：哦，那RESTful个什么概念？

应试者： 我不是说了吗，如果你使用 @RequestMapping(value=”/url”, method=”POST”)，你就是在开发RESTful应用。

我：哦，你对Hibernate如何？

应试者：我这两年一直在使用Hibernate。我对Hibernate很熟悉。

我：跟JDBC比起来，Hibernate有什么优势?

应试者：使用Hibernate，我们不需要写任何跟数据库交互的东西，Hibernate会帮我们处理这些。

我：那Hibernate怎么能知道你的项目需要如何的存取？

应试者：如果我们使用了Hibernate，它会帮我们完成存储，更新，取数据等数据库操作。

我：哦，哦。你在业余时间会读一些技术相关的博客吗？

应试者：当然，我对Hibernate的深入掌握就是这样学会的。

我：非常好，很高兴见到你。我们的人力资源部会给你打电话的。

面试过程就这样 …

我绝对相信各种框架会提高程序员的工作效率。但程序员也应该努力去了解这些框架是如何工作的。你并不需要理解各种框架的所有内部工作原理。如果你非 常的擅长Servlets和JSP，那你就很容易理解诸如Struts，Spring MVC等Java Web框架。如果你不了解这些基础知识，很显然，所有你的回答只能是“框架/标记/XML帮我们做了这些”。

我强烈建议所有刚开始职业生涯的Java程序员都要认真学习Java核心，Servlets，JSP知识。只有这样你才能正确的理解各种框架的工作原理。

####java程序会发生内存泄露的问题吗？请简单说说你的观点

答案：会。Java内存管理是通过垃圾收集器（Garbage Collection，GC）自动管理内存的回收的，java程序员不需要通过调用函数来释放内存。因此，很多人错误地认为Java不存在内存泄漏问题， 或者认为即使有内存泄漏也不是程序的责任，而是GC或JVM的问题。其实Java也存在内存泄露，但它的表现与C++语言有些不同。

java导致内存泄露的原因很明确：长生命周期的对象持有短生命周期对象的引用就很可能发生内存泄露，尽管短生命周期对象已经不再需要，但是因为长生命周期对象持有它的引用而导致不能被回收。

严格来说，内存泄漏就是存在一些被分配的对象，这些对象有下面两个特点，首先，这些对象是可达的，即在有向图中，存在通路可以与其相连；其次，这些 对象是无用的，即程序以后不会再使用这些对象。如果对象满足这两个条件，这些对象就可以判定为Java中的内存泄漏，这些对象不会被GC所回收，然而它却 占 用内存。

在java程序中容易发生内存泄露的场景：

  1.集合类，集合类仅仅有添加元素的方法，而没有相应的删除机制，导致内存被占用。这一点其实也不明确，这个集合类如果仅仅是局部变量，根本不会造成内存 泄露，在方法栈退出后就没有引用了会被jvm正常回收。而如果这个集合类是全局性的变量（比如类中的静态属性，全局性的map等即有静态引用或final 一直指向它），那么没有相应的删除机制，很可能导致集合所占用的内存只增不减，因此提供这样的删除机制或者定期清除策略非常必要。

   2.单例模式。不正确使用单例模式是引起内存泄露的一个常见问题，单例对象在被初始化后将在JVM的整个生命周期中存在（以静态变量的方式），如果单例对象持有外部对象的引用，那么这个外部对象将不能被jvm正常回收，导致内存泄露，考虑下面的例子：

　　class A{

　　public A(){

　　  B.getInstance().setA(this);

　　}

　　….

　　}

　　//B类采用单例模式

　　class B{

　　private A a;

　　private static B instance=new B();

　　public B(){}

　　public static B getInstance(){

　　return instance;

　　}

　　public void setA(A a){

　　this.a=a;

　　}

　　//getter…

　　}

显然B采用singleton模式，他持有一个A对象的引用，而这个A类的对象将不能被回收。想象下如果A是个比较大的对象或者集合类型会发生什么情况。

  所以在Java开发过程中和代码复审的时候要重点关注那些长生命周期对象：全局性的集合、单例模式的使用、类的static变量等等。在不使用某对象时，显式地将此对象赋空，遵循谁创建谁释放的原则，减少内向泄漏发生的机会。
  
  
  [JAVA面试13点经验](http://uule.iteye.com/blog/1119493)
  [阿里巴巴面试](http://www.thebigdata.cn/JiShuBoKe/979.html)
  [面试1](http://blog.csdn.net/liusocg520/article/details/21740463)
  [面试2](http://blog.csdn.net/lifetragedy/article/details/11898665)
  [面试3](http://www.mianwww.com/html/2011/09/10173.html)
