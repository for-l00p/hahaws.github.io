# const 限定符

我们希望一个变量它的值不被改变，可以用`const`对变量的类型加以限定

## 初始化

因为 const 对象创建后就不能再改变, 所以const对象必须初始化

## const的引用

可以把引用绑定在const上, 称之为`对常量的引用(reference to const)`

因为`引用不是对象, 只是对象的别名`, 所以const的引用就是对常量的引用

### 初始化和对const的引用

允许将const int& 绑定到一个非常量

```cpp
int i = 42;

// 正确,允许将const int& 绑定到一个非常量
const int &r1 = i;
// 正确, 42字面值是个常量, r2是常量引用
const int &r2 = 42;
// 正确, 常量和常量的计算结果仍然是常量, r3是常量引用
const int &r3 = r1 * 2;
// 错误, r4不是常量引用, 如果是对的, 那么可以通过修改r4的值,
// 显然是与预期相悖
int &r4 = r1 * 2;
```

## 指针和const

```cpp
#include <iostream>
using namespace std;


struct Date
{
    int year;
    int month;
    int day;
};

int main()
{
    // 常量 这个值不能修改，且在定义时指定初始值
    const int a = 10;

    // C语言需要struct，CPP不需要
    struct Date d = { 2011, 2, 5 };
    Date dt = { 2019, 12, 31 };

    const Date d1 = { 2012, 3, 12 };
    // 下面操作不允许，const 定义的结构体成员变量也不能修改
    d1.year = 2013;
    //  下面操作不允许，const 定义的结构体本身也不能修改
    Date d2 = { 2014, 2, 2 };
    d1 = d2;
    //
    // 非const限定的结构体变量可以用指针修改值
    Date *p = &dt;
    p->year = 2015;
    cout << dt.year << endl;

    const Date *ptr = &dt;
    // 用const限定指针本身，不能用指针修改结构体，以下操作不允许
    ptr->year = 2019;
    (*ptr).month = 12;
    *ptr = d1;

    // 以下指针分别代表什么含义
    int age = 10;
    const int *p = &age;
    int const *p1 = &age;
    int * const p2 = &age;
    const int * const p3 = &age;
    int const * const p4 = &age;

    //
    // 记住：const修饰的是他右边的内容
    // 1. const int *p = &age;
    // *p不能改，p可以改 p = &name;
    // 2. int const *p1 = &age;
    // p1不是常量，*p1是常量
    // 3. int * p2 = &age;
    // p2 是常量，*p2不是常量，可以通过*p2 = 20;修改其指向的值。但是，p2 = &name;不允许，p2是常量，其本身不允许修改
    //
    // const int * const p3 = &age;
    // p3是常量, *p3也是常量
    // p4, p5 是等价的

}
```

顶层const表示对象本身是常量(不能改变的)

底层const表示对象指向的对象是常量（不能改变）

```cpp
const char * const name = "fdfdf";
/*
 * 从右往左读
 * 有个变量name
 * name是个常量
 * name是个指针类型的常量
 * name是个指向char类型的指针常量
 * name是个指向的char是个常量
*/
```

## const & 在函数参数中的使用

```cpp
#include <iostream>
#include <string>

using namespace std;

struct People
{
    string name;
    int age;
};

/*
 * 函数参数是引用类型时就是给原来的变量起了别名在函数里使用
 * 函数里操作的还是变量本身，就是可以在函数里修改参数本身，这就是引用传递
 * 这种参数的好处就在于在函数栈中不会重新创建一个参数的拷贝，节约了空间
 */

void printPeople(People &p)
{
    cout << "name: " << p.name << "\n" << "age:  " << p.age << endl;
    return;
}

void haveBirthday(People &p)
{
    p.age += 1;
}

/*
 * 函数参数使用const& 类型时表示这个参数本身是不能修改的
 * 我们使用从右往左的方法去看
 * p首先是个引用，是个People类型的引用，并且它是const修饰的，不能改变
 */

// void constPeopleBirthday(const People & p)
// {
//     p.age += 1;
// }
//

// 和上面相同
// void constPeopleBirthday(People const & p)
// {
//     p.age += 1;
// }

int main()
{
    People p = { "John", 21 };
    printPeople(p);
    haveBirthday(p);
    printPeople(p);
    return 0;
}

```
