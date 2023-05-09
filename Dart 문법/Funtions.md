---
dg-publish: true
---

## Defining a Function
```dart
// 기본적인 함수 사용
returnType functionName (parameterType parameter) {}

// void는 return 값이 없을 때 사용하는 타입
void sayHi(String name) {
	print('Hi, $name');
} 

// 다른 내용 없이 바로 return 한다면 아래와 같이 사용도 가능 
void sayHi(String name) => 'Hi, $name';
String sayHello(String name) => 'Hello, $name';

```

## Named Parameters
- parmeter를 기본으로 사용하면 function을 만들때 입력한 순서대로 작성해야함 
	```dart
	// 아래와 같이 name, age, now 세 가지를 parameter로 받는 function이 있다
	void make(String name, int age, double percent) {}

	// 이 function을 사용하려면 parameter를 순서대로 type에 맞게 입력해야한다 
	make('hoi', 14, 2.4); 
	make(14, 'choi', 3); // 이렇게 사용하면 에러남
	```
- 위와 같은 순서대로 입력하려면 parameter가 어떤 순서로 어떤 type을 사용하는지 알아야하는 불편함이 있음
- Dart에서는 해결의 위해 name parameter를 사용함 
	```dart
	// 간단하게 parameter를 중괄호{} 로 감싸주면 됨
	void make({required String name, required int age, required double percent}) {}
	
	// 사용은 parameter name을 태그처럼 붙여주고 사용하면 됨
	make(name:'choi', age: 20, percent: 14.5);
	make(percent: 10, name:'park', age:14); // 순서를 바꿔서 입력해도 무관함 
	```
- named parameter는 required를 사용하지 않으면 모두 optional 사항이기 때문에 기본값을 입력해주지 않으면 null 사용이 허용되어야함 
	```dart
	void greeting({required String name, String country = 'korea', int? age}) => print('Hi, $name($age) from $country');
	
	// required가 사용된 name은 무조건 입력해야함
	// country는 korea라는 기본값을 가지기 때문에 입력을 하지 않으면 기본값이 사용됨
	// age는 기본값도 없기 때문에 입력하지 않으면 null값을 가지므로 type 뒤에 ?를 추가
	
	greeting(name: 'park'); // 출력 결과: Hi, park(null) from korea
	greeting(name: 'honda', country:'japan', age:14);
	// 출력 결과 : Hi, honda(14) from japan
	```
- parameter가 어떤 의미를 가지는지 알기 쉽고, 순서를 알아야할 필요가 없어 편리함

## Optional Positional Parameters
- positional parameter도 기본값을 주고 optional 로 설정해 줄 수 있음 
- named parameter가 사용하기 편해서 잘 사용되지는 않는 듯
	```dart
	void make(String name, int age) {}
	
	void make1(String name, [int? age = 12]){}
	// []안에 parameter를 넣고 null-safety와 기본값을 주면 optional로 설정이 됨 
	```

## QQ Operator
> Dart에는 다양한 operator들(??, ?=, !=, ||, 등)이 존재하지만 그 중에서 몇가지만 설명을 함

```dart
// 1. if를 사용한 null check
String capitalizeName(String? name) {
	if(name != null) {
		return name.toUpperCase(); // name을 대문자화 
	}
	return 'ANON'; // null 이면 'ANON'을 return 
}
// 2. 삼항연산자를 사용한 null check
// 조건문 ? true : false  형식으로 사용
String capitalizeName(String? name) => name != null ? name?.toUpperCase() : 'ANON';

// 3. ?? 연산자를 사용한 null check
// a ?? b : a가 null이 아니면 a를 반환, a가 null이면 b를 반환
String capitalizeName(String? name) => name?.toUpperCase() ?? 'ANON';

// ??= 
String? name; 
name ??= 'ANON';
// name 이 null 이면 'ANON'을 name에 넣음 

```


## Typedef
> 자료형에 사용자가 원하는 alias(별명)을 붙일 수 있음 

```dart
List<int> reverseListOfNum(List<int> list) {
	var reverse = list.reversed;
	return reverse.toList();
}

typedef ListOfInt = List<int>;

ListOfInt reverseListOfNum(ListOfInt list) {
	var reverse = list.reversed;
	return reverse.toList();
}

// 위와 아래는 같은 코드이지만 typedef를 사용하여 자료형을 나만의 이름을 붙여 사용하고있다.

```
