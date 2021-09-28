# Shallow copy and Deep copy

## **Shallow Copy**

When an object is created by just copying the data of the original object, then it is called a shallow copy of the object. The data copied includes all the data members of the associated class.
By default, C++ performs shallow copy by implicitly creating a copy constructor and overloaded assignment operator.
Shallow copy works well when our class is simple i.e. when the variables of the object are not dynamically allocated. If any variable of the original object is dynamically allocated, then the shallow copy will also reference to the same memory location. Therefore, the changes made in one of the objects will be reflected on the other object also.

### Pros -

- Shallow copy is faster and simpler.

### Cons -

- Shallow copy may create ambiguity and dangling pointers due to sharing of same memory location for dynamically allocated variables.

### Example

```
#include<iostream>
using namespace std;

class Contributor{
    private:
        string domain;
        int batchNo;
        int contributions;
    public:
        void setInfo(string dName, int batchNo, int count)
        {
            domain = dName;
            this->batchNo = batchNo;
            contributions = count;
        }
        void display()
        {
            cout<<"Name of domain: "<<domain<<endl;
            cout<<"Batch number: "<<batchNo<<endl;
            cout<<"Number of contributions: "<<contributions<<endl;
        }
};
int main()
{
    Contributor c1, c2;
    c1.setInfo("C/CPP", 1, 5);
    cout<<"Object c1 \n";
    c1.display();
    //assignment operator
    c2 = c1;
    cout<<"Object c2 \n";
    c2.display();
    //copy constructor
    Contributor c3 = c1;
    cout<<"Object c3 \n";
    c3.display();
    return 0;
}
```
