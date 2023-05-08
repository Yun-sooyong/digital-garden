---
{"dg-publish":true,"permalink":"/dart/data-type/"}
---



## Basic Data Type
- String : 문자열 
- bool : true or false 
- int : 정수
- double : 실수
- num : int or double (int와 double은 모두 num을 상속받음)

## Lists
>데이터를 순차적으로 담을 수 있는 검색 가능한 자료구조
```dart
var numList = [1,2,3,4];
List<int> numList2 = [1,2,3,4]; // 타입 명시 List<int> int형을 가지는 List타입

print(numList[0]); // 1, index의 값을 검색해서 가져올 수 있음
```
- ##### property
	```dart
	var numList = [1,2,3,4];
	
	numList.first; // 가장 앞에있는 item을 가져옴
	numList.last;  // 가장 마지막의 item을 가져옴
	numList.isEmpty; // List가 비어있는지 확인해서 true, false를 반환
	numList.length; // List의 길이를 반환 
	
	// 기타 여러가지 기능들이 존재
	```
- ##### method

	```dart
	var numList = [1,2,3,4];
	
	numList.add(5); // List의 맨 뒤에 5를 추가 [1,2,3,4,5]
	numList.addAll([6, 7]); // List의 맨 뒤에 6, 7을 추가 [1,2,3,4,5,6,7]
	numList.clear(); // List의 모든 내용물을 제거
	
	// 이외에도 많은 기능이 존재 
	```

- ##### collection if
	```dart
	var giveMeFive = true;
	
	var list = [1,2,3,4, if(giveMeFive) 5,];
	
	//if(giveMeFive) list.add(5); = if(giveMeFive) 5
	// 두 가지는 같은 결과값을 가짐
	```
- ##### collection for
	* List 안에서 for문을 사용할 수 있음
	```dart
	var cats = ['tiger', 'cat', 'lion'];
	var animal = ['dog', 'pig', 'cow', 'horse', 
			 for(var cat in cats) 'cats_$cat',];
	print(animal); // [dog, pig, cow, horse, cats_tiger, cats_cat, cats_lion]
	```
## String Interpolation
>텍스트에 변수를 추가하는 방법
- $ 기호를 사용해서 문자열의 중간에 변수값을 삽입할 수 있음 
	```dart
	var name = 'Fione';
	
	var greeting = 'Hello everyone my name is $name.';
	// $기호 뒤에는 변수를 삽입해야함 
	
	var nameLength = 'My name is $name, length is ${name.length}';
	// 변수에 계산을 하거나 다른 동작를을 추가하고 싶으면 $뒤에 {}를 사용하면 됨
	```

## Maps
> key와 value의 형태로 연결해서 데이터를 저장 
> key와 value 모두 모든 유형의 객체가 될 수 있음 
> key는 중복이 안되지만 value는 동일한 값을 사용할 수 있음
```dart
var maps = {
1: 'one',
2: 'two',
3: 'three',
} 
// Map<int, String> 형식의 map 생성 

var map1 = {
'one': 1,
'two': true,
'three': 'third', 
'list': [1,2,3,4],

// map1의 경우 Map<String, Object>형식을 가지게 됨 
// Object는 최상위 클래스로 Dart의 모든 클래스가 Object를 상속받음 
// 따라서 Object는 모든 유형의 자료형을 사용할 수 있음 
// 다양한 객체를 사용할 수 있어 Map에 List나 Map을 넣을 수도 있음

Map<int, bool> map2 = {
1: true,
2: false,
3: false,
}
// 명시적으로도 사용이 가능
``` 

## Sets
> List와 비슷하지만 Set은 item의 중복을 허용하지 않아 item들이 모두 유니크 해야함 
```dart
// set도 var를 사용하거나 직접 명시해서 만들 수 있음 
var set1 = {'item1', 'item2', 'item3'};
Set<String> set2 = {'itme1', 'item2', 'item3'}; 

List list = ['item1', 'item2', 'item1']; // list는 가능 
Set set3 = {'item1', 'item2', 'item1'}; // set은 불가능 

var a = [1,2]; // list
var b = {1,2}; // set
```

<br>

[[home\|home]] 

---
#Dart