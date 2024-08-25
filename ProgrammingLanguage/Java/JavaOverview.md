# Java 中的关键字

## final

final可以用来修饰variable,method和class
1. variable
    1. 一个永不改变的编译时常量
    2. 一个在运行时被初始化的值， 而你不希望它被改变
2. method
    1. 把方法锁定，以防止任何继承类修改它的含义，确保在继承中使方法行为保持一变，并且不会被覆盖
    2. 效率
    3. 类中，所有的private方法都隐式地指定为final，由于无法取用private方法，所以也就无法覆盖它
3. class
    1. 表明你打算继承该类，而且也不允许别人这样做，换句话说，该类的设计永不需要做任何变动，或者处于安全的考虑， 你不希望他有子类

对final有新的认知了

当用 **`final`** 修饰一个变量时，表示该变量的值不能被修改。这可以应用于实例变量、类变量（静态变量）或局部变量。

```java
class Example {
    final int constantVariable = 10; // 实例变量
    static final double PI = 3.14159; // 类变量（静态变量）

    void method() {
        final int localVar = 5; // 局部变量
        // localVar = 8; // 不能修改 final 变量的值
    }
}
```

注意：对于引用类型的变量，**`final`** 表示该变量不能被重新分配引用，但是对象的状态（即对象中的字段）仍然可以被修改。

```java
final List<String> myList = new ArrayList<>();
myList.add("Item 1"); // 可以修改列表的内容
// myList = new ArrayList<>(); // 不能重新分配 myList 的引用
```

当使用 **`final`** 修饰引用类型的变量时，意味着该变量所引用的对象不能被重新分配引用。这是指不能让这个变量指向另一个对象。但是，被引用的对象本身的状态（即对象内部的字段值）仍然是可变的，可以进行修改。

```java
final List<String> myList = new ArrayList<>();
myList.add("Item 1");

// 不能重新分配 myList 的引用
// myList = new ArrayList<>(); // 这行代码会引发编译错误

// 但是可以修改 myList 引用的对象的状态
myList.add("Item 2");
```

在上面的例子中，**`myList`** 是一个 **`final`** 引用，因此不能通过 **`myList = new ArrayList<>();`** 这样的语句来重新分配引用，这会导致编译错误。但是，可以使用 **`myList.add("Item 2");`** 来修改 **`myList`** 引用的 **`ArrayList`** 对象的状态，向其中添加新的元素。