# Shallow copy and Deep copy

## **Shallow Copy**

When an object is created by just copying the data of the original object, then it is called a shallow copy of the object. The data copied includes all the data members of the associated class.</br>
By default, C++ performs shallow copy by implicitly creating a copy constructor and an overloaded assignment operator.</br>
Shallow copy works well when our class is simple i.e. when the variables of the object are not dynamically allocated. If any variable of the original object is dynamically allocated, then the shallow copy will also reference to the same memory location. Therefore, the changes made in one of the objects will be reflected on the other object also.

<p align="center"> <img src="https://user-images.githubusercontent.com/61552413/135149241-49f25064-5ff7-4516-95e3-9f942d1d9792.png" height="350"> </p>

### Example

```
#include<iostream>
using namespace std;

class Contributor{
    private:
        string domain;
        int batchNo;
        int *contributions;
    public:
        Contributor(string dName, int batchNo, int count)
        {
            domain = dName;
            this->batchNo = batchNo;
            contributions = new int;
            *contributions = count;
        }
        void display()
        {
            cout<<"Name of domain: "<<domain<<endl;
            cout<<"Batch number: "<<batchNo<<endl;
            cout<<"Number of contributions: "<<*contributions<<endl;
        }
        void setValue(int count)
        {
            *contributions = count;
        }
        ~Contributor()
        {
            delete contributions;
        }
};
int main()
{
    Contributor c1("C/CPP", 1, 5);
    cout<<"Object c1\n";
    c1.display();
    //copy constructor
    Contributor c2 = c1;
    cout<<"Object c2\n";
    c2.display();
    //change made in object c1
    c1.setValue(10);
    cout<<"Object c1\n";
    c1.display();
    //change would be reflected in object c2 also
    cout<<"Object c2\n";
    c2.display();
    return 0;
}
```

### Output

```
Object c1
Name of domain: C/CPP
Batch number: 1
Number of contributions: 5
Object c2
Name of domain: C/CPP
Batch number: 1
Number of contributions: 5
Object c1
Name of domain: C/CPP
Batch number: 1
Number of contributions: 10
Object c2
Name of domain: C/CPP
Batch number: 1
Number of contributions: 10
```

### Advantage

- Shallow copy is faster and simpler.

### Disadvantage

- Shallow copy may create ambiguity and dangling pointers due to sharing of same memory location for dynamically allocated variables.
