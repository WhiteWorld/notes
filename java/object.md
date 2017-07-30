# Object

所有类的父类

## 方法

getClass 返回对象的运行时类的信息

hashcode equals

- equals 相同 hashcode 必须相同
- equals 不同 hashcode 不一定要不同，为了hash的效率最好也不同

实现 hashcode 方法， 使用

``` Java
@Override
public int hashCode(){
    return Objects.hashCode(this.firstName, this.lastName);
}
```

clone

浅拷贝、深拷贝

toString

默认实现, 推荐所有子类都覆盖这个方法

``` Java
 public String toString() {
        return getClass().getName() + "@" + Integer.toHexString(hashCode());
    }
```

notify()  wait()

- 必须在 synchronized 中使用，锁定的对象是同一个
- wait 需要下 while 中使用

linux的pthread_cond_wait是用futex系统调用，这个是慢速系统调用，看过apue知道任何慢速系统调用被信号打断的时候会返回-1，并且把errno置为EINTR，如果慢速系统调用的重启功能被关闭，需要在调用该系统调用的地方手动重启它，像下面这样：

while (1) {
    int ret = syscall();
    if (ret < 0 && errno == EINTR)
        continue;
    else
        break;
}

但是futex不能这么用，因为futex结束后到再次重启这个过程有个时间窗，在这个窗口内可能发生了pthread_cond_signal/phread_cond_broadcast，如果发生这种情况，再进行pthread_cond_wait的时候就错过了一次条件变量的变化，就会无限等待下去。但是如果不像上面那样写又无法重启futex系统调用，咋整呢？这就回到了上面检查布尔条件的时候为什么用while而不用if。

Wait immediately looses the lock, whereas Nofity will leave the lock only when the ending bracket is encountered.

自旋锁：当发生争用时，若Owner线程能在很短的时间内释放锁，则那些正在争用线程可以稍微等一等（自旋），在Owner线程释放锁后，争用线程可能会立即得到锁，从而避免了系统阻塞。但Owner运行的时间可能会超出了临界值，争用线程自旋一段时间后还是无法获得锁，这时争用线程则会停止自旋进入阻塞状态（后退）。基本思路就是自旋，不成功再阻塞，尽量降低阻塞的可能性，这对那些执行时间很短的代码块来说有非常重要的性能提高。自旋锁有个更贴切的名字：自旋-指数后退锁，也即复合锁。很显然，自旋在多处理器上才有意义。在线程进入ContentionList时，自旋
偏向锁：cas 写 thread id, 一次cas
轻量级锁：对象头添加指向锁的指针，锁记录是Mark Word, 多次cas
重量锁：cxq entryList waiterList，cas 导致 cache 对齐，有性能开销

finalize

protected void finalize() throws Throwable {}
- every class inherits the finalize() method from java.lang.Object
- the method is called by the garbage collector when it determines no more references to the object exist
- the Object finalize method performs no actions but it may be overridden by any class
- normally it should be overridden to clean-up non-Java resources ie closing a file
- if overridding finalize() it is good programming practice to use a try-catch-finally statement and to always call super.finalize(). This is a safety measure to ensure you do not inadvertently miss closing a resource used by the objects calling class

``` Java
protected void finalize() throws Throwable {
     try {
         close();        // close open files
     } finally {
         super.finalize();
     }
 }
 ```

- any exception thrown by finalize() during garbage collection halts the finalization but is otherwise ignored
- finalize() is never run more than once on any object