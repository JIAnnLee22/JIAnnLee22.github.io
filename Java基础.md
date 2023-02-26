# Java基础

## ==、equals区别

基础数据类型只有==操作符用来比较值是否相同;  
而对于引用类型来说==操作符就是地址比较了，`equals`如果没有重写则是跟`==`没有区别;  
正常类似String和基础类型封装的引用类型都是先比较地址是否相同，再比较值是否相同。  
没有重写`equals`的类则是Object类的的地址比较。  
以Java为例  
```java
// String
public boolean equals(Object anObject) {
    if (this == anObject) {//地址比较
        return true;
    } else {
        if (anObject instanceof String) {
            String aString = (String)anObject;
            if (this.coder() == aString.coder()) {
                return this.isLatin1() ? StringLatin1.equals(this.value, aString.value) : StringUTF16.equals(this.value, aString.value);
            }
        }
        return false;
    }
}
    
// Object
public boolean equals(Object obj) {
    return this == obj;//地址比较
}
```

