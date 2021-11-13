# Ambiguity in Hybrid inheritance

## What is Hybrid inheritance and its ambiguity?

Hybrid inheritance is followed when we combine more than one different type of inheritance. It is also known as virtual inheritance. Following image shows an example of hybird inheritance. It shows a combination of hierarchial and multiple inheritance.

<p align="center"> <img src="https://user-images.githubusercontent.com/61552413/141612218-e68f2c7f-d3d4-46da-a060-bc50eba9f085.png" height="350"> </p>

```
#include<iostream>
using namespace std;
class A{
    public:
    int a;
};
//Hierarchial inheritance
class B : public A{
    public:
    int b;
};
class C : public A{
    public:
    int c;
};
//Multiple inheritance
class D : public B, public C{
    public:
    int d;
};
int main()
{
    D objD;
    //Error => objD.a = 10; can't access 'a' directly
    objD.B::a = 10;
    objD.C::a = 20;
    objD.b = 20;
    return 0;
}
```

Here, class B and class C both inherit class A via multiple inheritance. Both class B and class C will have a seperate single copy of class A with them. But class D will contain two copies of class A and would hence lead to ambiguity in data. Therefore, when accessing data of class A from an object of class D, we need to specify the path through which that data would be accessed, i.e. either via class B or via class C.

## How to resolve this ambiguity?

### 1. By using scope resolution operator ( : : )

The above example uses scope resolution operator to differentiate between the different values of 'a'.

### 2. By using virtual base class

Virtual base class is used in virtual inheritance to avoid multiple occurances of a particular class in a hierarchy. Here, if class A is inherited virtually then, only one copy of its data would be inherited in class B and C. Hence, when virtual base class is used, only one copy will be shared. This can be demonstrated in the below example :

```
#include<iostream>
using namespace std;
class A{
    public:
    int a;
    A() //constructor
    {
        a = 10;
    }
};
//using class A as a virtual base class
class B : virtual public A{
    public:
    int b;
};
//using class A as a virtual base class
class C : virtual public A{
    public:
    int c;
};
class D : public B, public C{
    public:
    int d;
};
int main()
{
    D objD;
    cout<<"The value of 'a' from class A : "<<objD.a;
    return 0;
}
```

Output:

```
The value of 'a' from class A : 10
```
