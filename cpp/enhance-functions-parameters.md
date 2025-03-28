# Enhance functions parameters
- When you pass parameters in most of high level languages, you don't think about how it passed, because in general there is specific way language treat with the variables and asigned values.
- Here in C++ things is different, If you pass the argument to your function in in a wrong way it can cost you un nessessary operations, so now we will see different ways to deal with passing parameters.

## Pass the parameter as a Value
- When you pass the parameter as a value it will copied, and then passed.
- If the you pass huge data or object like so long **String** it will cost you so mutsh to copy then pass.
- It's prefered to use with cheap data like *int*, *char*, *bool*, *double*.
- Don't use it with values that it's size > sizeof(veid*) * 2.

### Example
```cpp
double sum(double num1, double num2) // ✅ Because double is cheap.
vector<bool> num_greater_than_0(vector<int> nums) // ❌ Because vector can be so huge and it will be high cost to copied.
```
## Pass the parameter as a lvalue reference
- When you pass the parameters as a rvalue reference, it means that the parameter point to the same location argument point to. and prevent the parameter to copy the value of the argumetns.
- It's good for huge sized objects, like *String*, *vector*, *array*, etc.
- It's bad approch for low sized objects, because it just make overhead without great benifit. low sized objects or data types can be like: *bool*, *int*, *char*, *double*.
- Don't use it with values it's size <= sizeof(void*) * 2.

### Example
```cpp
double sum(double& num1, double& num2) // ❌ Because double is cheap and reference is expensive, and it also add unneccessary indirect for the argument.
vector<bool> num_greater_than_0(vector<int>& nums) // ✅ Because vector can be so huge and it will be high cost to copied, reference will avoid unneeded copy.
```

## Pass the parameter as a rvalue reference
- When you pass the parameters as a rvalue reference, it means that the parameter transfare the ownership of the resource of the original variable to the parameter, and the old varibale will be no longer asigned to the value. and prevent the parameter to copy the value of the argumetns.
- It's good for huge sized objects, like *String*, *vector*, *array*, etc.
- It's bad approch for low sized objects, because it just make overhead without great benifit. low sized objects or data types can be like: *bool*, *int*, *char*, *double*.
- Don't use it with values it's size <= sizeof(void*) * 2.

### Example
```cpp
double sum(double& num1, double& num2) // ❌ Because double is cheap and lvalue reference is expensive, and it also add unneccessary indirect for the argument.
vector<bool> num_greater_than_0(vector<int>&& nums) // ✅ Because vector can be so huge and it will be high cost to copied, lvlaue reference will avoid unneeded copy.
```
## Save your original data from modification
- You can use `const` keyword to prevent parameter of a varible from changing.
### Example
```cpp
const double PI = 22/7;
vector<string> add_prefix(const vector<string>& words);
```
## What is the difference between lvalue and rvalue references?
- Both references prevent coping of your valuable value.

### Lvalue reference `type&`
- Lvalue reference it refer to the same location the original variable refere.
#### Example
```cpp
string a = "Ahmed Al-3adl";
string& b = a; // Asign lvalue reference *b* to the left-value a
```
-  Lvalue reference cannot bind to rvalues.
#### Example
```cpp
string full_name(string& first_name, string& last_name)
full_name("Ahmed", "Al-3adl"); // ❌ ERROR: Cannot bind rvalue to lvalue reference
```
### Rvalue reference `type&&`
- Rvalue reference it refer to the same location the original variable refer, but chang the originla variable to refer to nothing.
#### Example
```cpp
string a = "Ahmed Al-3adl";
string&& b = std::move(a); // You need std::move because it's not normal for rvalue reference to refer to left-value(variable) 
```
- It you try to refer to right-value(un asigned value) it will asigned temporary to some location in the memory.
#### Example
```cpp
string full_name(string&& first_name, string&& last_name);
full_name("Ahmed", "Al-3adl"); // ✅ It will work
```
- *Note*: if you ask your selfe what about if I pass rvalue to a noramal parameter that will take it as a value. The noremal parameter will copy it.
#### Example
```cpp
string full_name(string first_name, string last_name);
full_name("Ahmed", "Al-3adl"); // ✅ It will work and the data will copied
```
### what we mean by rvalue and lvalue
#### Rvalue => Right value
- We mean it the value the be in the right of asign operator `=` and it at most times is a pure values.
##### Example
```cpp
int a = 9; // You can see 9 in the right of the asign operator.
```
#### Lvalue => Left value
- We mean it the value that be in the left of asign operator `=` and it always a variable.
##### Example
```cpp
int a = 9; // You can see a in the left of the asign operator.
```