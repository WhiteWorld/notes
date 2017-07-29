# String

实现 Serializable Comparable<String> CharSequence，内部是 final char value[] 保证 immutable

## trim

trim() 中 char[] val = value;    /* avoid getfield opcode */

## equals

```Java
public boolean equals(Object anObject) {
        if (this == anObject) {
            return true;
        }
        if (anObject instanceof String) {
            String anotherString = (String)anObject;
            int n = value.length;
            if (n == anotherString.value.length) {
                char v1[] = value;
                char v2[] = anotherString.value;
                int i = 0;
                while (n-- != 0) {
                    if (v1[i] != v2[i])
                        return false;
                    i++;
                }
                return true;
            }
        }
        return false;
    }
```
contentEquals

## intern

- 直接使用双引号声明出来的String对象会直接存储在常量池中。
- 如果不是用双引号声明的String对象，可以使用String提供的intern方法。intern 方法会从字符串常量池中查询当前字符串是否存在，若不存在就会将当前字符串放入常量池中
- JDK 1.6 常量池是放在 Perm 区中的, 1.7 之后字符串常量池已经从 Perm 区移到正常的 Java Heap 区域了
- 将String常量池 从 Perm 区移动到了 Java Heap区String#intern 方法时，如果存在堆中的对象，会直接保存对象的引用，而不会重新创建对象。

参考 [深入解析String#intern](https://tech.meituan.com/in_depth_understanding_string_intern.html)

## 私有构造函数，性能高

```
String(char[] value, boolean share) {
        // assert share : "unshared not supported";
        this.value = value;
    }
```

## 关于编码

- unicode是一种“编码”，所谓编码就是一个编号(数字)到字符的一种映射关系，就仅仅是一种一对一的映射而已，可以理解成一个很大的对应表格
- GBK、UTF-8是一种“编码格式”，是用来序列化或存储1中提到的那个“编号(数字)”的一种“格式”；GBK和UTF-8都是用来序列化或存储unicode编码的数据的，但是分别是2种不同的格式； 他们俩除了格式不一样之外，他们所关心的unicode编码范围也不一样，utf-8考虑了很多种不同国家的字符，涵盖整个unicode码表，所以其存储一个字符的编码的时候，使用的字节长度也从1字节到4字节不等；而GBK只考虑中文——在unicode中的一小部分——的字符，的编码，所以它算好了只要2个字节就能涵盖到绝大多数常用中文(2个字节能表示6w多种字符),所以它存储一个字符的时候，所用的字节长度是固定的；

# StringBuilder

继承 AbstractStringBuilder 实现 java.io.Serializable, CharSequence

## AbstractStringBuilder 

abstract class AbstractStringBuilder implements Appendable, CharSequence

append insert 底层实现都是调用的 arrayCopy native 方法

默认初始 capacity 值 16, 扩容后是当前数组长度2倍+1

## StringBuffer

同步方法，线程安全

## + vs StringBuilder

如果结构比较简单编译器会自动替换 + 为 StringBuilder append，如果结构比较复杂如循环，应该使用StringBuilder。使用StringBuilder时候，不要混着使用 +，否则会创建更多的StringBuilder。

http://www.blogjava.net/nokiaguy/archive/2008/05/07/198990.html