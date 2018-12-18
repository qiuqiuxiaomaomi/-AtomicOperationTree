# AtomicOperationTree
Java原子操作技术研究

###原子更新基本操作

![](https://i.imgur.com/bhBZbWo.png)

最终调用了native方法来保证更新的原子性

<pre>
          当更新一个变量时，多出现数据争用的时候可能出现意想不到的情况，这时一般的策略是
      使用synchronized解决，因为synchronized能够保证多个线程不会同时更新该变量。然而
      jdk1.5之后，提供了粒度更新，更轻量级，并且在多核处理器具有更高性能的原子操作类。因为
      原子操作类把竞争的范围缩小到单个变量上，这可以说是粒度最细的情况了。

          原子操作类相当于泛化的volatile变量，能够支持原子读取-修改-写操作。原子操作类有
      13个类，在java.util.concurrent.atomic包下，可以分为四种类型的原子更新类：
          1）原子更新基本类型
             AtomicBoolean   原子更新布尔变量
             AtomicInteger   原子更新整型变量
             AtomicLong      原子更新长整型变量

          2）原子更新数组类型
             AtomicIntegerArray   原子更新整型数组的某个元素
             AtomicLongArray      原子更新长整型数组的某个元素
             AtomicReferenceArray    原子更新引用类型数组的某个元素

             数组value通过构造的方式传入AtomicIntegerArray中，实际上AtomicIntegerArray会
             将当前数组拷贝一份，所以在数组拷贝的操作不影响原数组的值。

          3）原子更新引用
             AtomicReference   原子更新引用类型
             AtomicReferenceFieldUpdater    原子更新引用类型里的字段
             AtomicMarkableReference     原子更新带有标记位的引用类型

          5）原子更新属性
             AtomicIntegerFieldUpdater  原子更新整型字段
             AtomicLongFieldUpdater     原子更新长整型字段
             AtomicStampedReference     原子更新带有版本号的引用类型

             要想原子更新字段，需要两个步骤：
                 1）每次必须使用newUpdater创建一个更新器，并且需要设置想要更新的类的字段
                 2）更新类的字段（属性）必须为public volatile
</pre>