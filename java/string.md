String

实现 Serializable Comparable<String> CharSequence

内部是 final char value[] 保证 immutable

trim() 中 char[] val = value;    /* avoid getfield opcode */

equals

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

intern

- 直接使用双引号声明出来的String对象会直接存储在常量池中。
- 如果不是用双引号声明的String对象，可以使用String提供的intern方法。intern 方法会从字符串常量池中查询当前字符串是否存在，若不存在就会将当前字符串放入常量池中
- JDK 1.6 常量池是放在 Perm 区中的, 1.7 之后字符串常量池已经从 Perm 区移到正常的 Java Heap 区域了
- 将String常量池 从 Perm 区移动到了 Java Heap区String#intern 方法时，如果存在堆中的对象，会直接保存对象的引用，而不会重新创建对象。

参考 [深入解析String#intern](https://tech.meituan.com/in_depth_understanding_string_intern.html)

