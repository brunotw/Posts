---
marp: true
author: Bruno Willian
theme: default
#class: invert 
size: 16:9
title: Connect to Dataverse through powershell
backgroundImage: url('https://github.com/brunotw/Posts/blob/main/Backgrounds/Slide6.PNG?raw=true')
---
#  C# Basics - Preventing NullReferenceException
---
# Null-conditional operators
Available in C# 6 and later, a **_null-conditional operator (?. and ?[])_** allows the expression to check the property before accessing its instance. 

The null-conditional operators are short-circuiting. That is, if one operation in a chain of conditional member or element access operations returns null, the rest of the chain doesn't execute.  

---
### Take classes below for our example
```c#
public class ClassA
{
    public ClassB ClassB { get; set; }
}

public class ClassB
{
    public bool IsActive() { return true; }
}
```

---
### Null-conditional operator ?.
```c#
// Instanciating a new Class A. ClassB property will be Null
ClassA classA = new ClassA();

// Object reference not set to an instance of an object
bool isActive = classA.ClassB.IsActive(); 

// Apply Null-conditional operator and make isActive nullable
// ClassB is evaluated to null so IsActive isn't called.
bool? isActive = classA.ClassB?.IsActive();
bool isActive2 = classA.ClassB?.IsActive() ?? false;
```
---
### Null-conditional operator ?[]

```c#
// GetOrders method might return null
IList<double> orders = GetOrders();

// If orders isn't null, call Sum() otherwise return 0
double total = orders?.Sum() ?? 0;

// Note that for collections if you try to access an item outside the 
// bounds, it  will throw IndexOutOfRangeException.
double total = orders?[x];
```

---
>>>>>>>>>>>># Thank you 
>>> Hopefully now you are one step further from NullReferenceException


