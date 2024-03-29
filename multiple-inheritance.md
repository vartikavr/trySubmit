# Multiple inheritance

Multiple inheritance is a type of inheritance in which a class can inherit from more than one class.

Therefore, in multiple inheritance, the derived class can access the different data members and member functions of its base classes according to the defined access modes. The access modes are defined using access specifiers. There are three access specifiers that can be used in inheritance in C++, they are: private, protected, and public.

The below image demonstrates a simple example of multiple inheritance :

<p align="center"> <img src="https://user-images.githubusercontent.com/61552413/142762283-e4deada2-c86b-433a-9e54-8cb05ff99f31.png" height="350"> </p>

Here, class D will be regarded as a child class or derived class, and classes A, B and C will be regarded as the parent classes or the base classes.

A real-life example of multiple inheritance could be, class Bat inheriting its properties and characteristics from classes Mammal and wingedAnimal.

## Example

```cpp
#include <iostream>
using namespace std;

class A
{
    int a;
    public:
    void callA()
    {
        cout<<"Inside Class A\n";
    }
};
class B
{
    int b;
    public:
    void callB()
    {
        cout<<"Inside Class B\n";
    }
};
//Multiple inheritance
class C: public A, public B
{
  int c;
  public:
  void callC()
  {
      cout<<"Inside Class C\n";
  }
};

int main() {
	C obj;
	//All the three functions can be accessed via Class C's object
	obj.callA();
	obj.callB();
	obj.callC();
	return 0;
}
```

Output :

```
Inside Class A
Inside Class B
Inside Class C
```

## Constructors and Destructors in multiple inheritance

The constructors of base classes in multiple inheritance are called in the sequence in which they are inherited. The base class declared first during inheritance will invoke its constructor first, the one declared second will invoke after that, and so on. The opposite order will be followed for the destructors.

### Example

```cpp
#include <iostream>
using namespace std;

class A
{
    public:
    A()
    {
        cout<<"Constructor of Class A\n";
    }
    ~A()
    {
        cout<<"Destructor of Class A\n";
    }
};
class B
{
    public:
    B()
    {
        cout<<"Constructor of Class B\n";
    }
    ~B()
    {
        cout<<"Destructor of Class B\n";
    }
};
//Multiple inheritance
class C: public B, public A
{
  public:
  C()
  {
      cout<<"Constructor of Class C\n";
  }
  ~C()
  {
      cout<<"Destructor of Class C\n";
  }
};
int main() {
	C obj;
	return 0;
}
```

Output :

```
Constructor of Class B
Constructor of Class A
Constructor of Class C
Destructor of Class C
Destructor of Class A
Destructor of Class B
```

## Disadvantages of multiple inheritance

- It may lead to complex structures and relationships between classes.
- It may lead to ambiguity.
