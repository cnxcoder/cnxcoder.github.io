---
layout: post
title:  "Lambda in C++ 11"
date:   2016-17-03 11:00:00 +0700
categories: cpp11 beginer
---

# Lambda in C++ 11

แลมดา คือการเขียน anonymous function แบบ inline. ทำให้สะดวกในการโค๊ดยิ่งขึ้น

#### Syntax

```cpp
	[](){}
	[capture](parameters)  return_type -> { function_body }
```
[]  คือ lambda capture block.

[] ใช้ระบุว่าให้แลมดามีการเก็บค่าใดในบล๊อกสโคปทีมันอยู่เอาเข้าไปด้วย ถ้าไม่ระบุก็คือไม่มีการเก็บค่าใดๆ

```cpp
	auto hello = []() {std::cout<<"Hello Lambda"<<std::endl;};
	hello();
```

[x] หากมีการระบุชื่อตัวแปรโดยจะเป็นเก็บค่าแบบ by value

```cpp
	string name = "Hello Lambda";
	auto info = [name](){cout<<name<<endl;};
	info();
```

[&x] หากมีการระบุ & หน้าชื่อตัวแปรโดยจะเป็นเก็บค่าแบบ by reference

```cpp
	string name = "Hello Lambda";
	auto info = [&name](){ name = "name changed"; cout<<name<<endl;};
	info();
```

[=] เป็นการระบุให้เก็บค่าทั้งหมดในบล๊อกสโคป แบบ by value

```cpp
	int main()
	{
		string name = "Hello Lambda";
		int decNum = 123;
		double realNum = 456.78;

		auto info = [=]()
		{	cout<<name<<endl;
			cout<<decNum <<endl;
			cout<<realNum <<endl;};

		info();
		
		cout << name << endl;
		cout << decNum << endl;
		cout << realNum << endl;

		return 0;
	}
```

[&] เป็นการระบุให้เก็บค่าทั้งหมดในบล๊อกสโคป แบบ by reference

```cpp
	int main()
	{
		string name = "Hello Lambda";
		int decNum = 123;
		double realNum = 456.78;

		auto info = [&]()
		{	name = "changed";
			age = 456;
			gpa = 89.99;};

		info();
		cout << "----after lambda execution---\n";
		cout << name << endl;
		cout << age << endl;
		cout << gpa << endl;

		return 0;
	}

```


()  คือ lambda paremeters

ถ้าไม่มีพารามิเตอร์นั้น จะใส่วงเล็บหรือใม่ก็ได้

เช่น 

```cpp
	auto hello = []{std::cout<<"Hello Lambda"<<std::endl;};
	hello();
```

หรือ

```cpp
	auto hello = []() {std::cout<<"Hello Lambda"<<std::endl;};
	hello();
```

ในกรณีที่ แลมดามี พารามิเตอร์ 

```cpp
	auto sum = [](int a, int b){std::cout<<a + b <<std::endl;};
	sum(5,6);
```

ในกรณีที่มีการรีเทิร์นค่า ก็ระบุชนิด return type ที่หลังวงเล็บ

```cpp
	auto sum = [](int a,int b)->int{return a+b;};
	cout<<sum(1,2);
```

ในกรณี่ที่ไม่มีการระบุค่ารีเทิร์น คอมไพเลอร์จะหาว่าจะต้องคืนค่าชนิดใดเอง ( duduction process)

```cpp
	auto multiply = [](double a , int b){return a * b;}; //return as double;
	cout<<sizeof(multiply(3,4))<<endl; 
```


## References

[http://en.cppreference.com/w/cpp/language/lambda](http://en.cppreference.com/w/cpp/language/lambda)

[http://en.cppreference.com/w/cpp/utility/functional/function](http://en.cppreference.com/w/cpp/utility/functional/function)


