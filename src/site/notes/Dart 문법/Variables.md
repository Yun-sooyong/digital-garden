---
{"dg-publish":true,"permalink":"/dart/variables/"}
---

>Dart 에서는 관습적으로 함수, 메서드에서는 var, class에서는 타입을 명시


## var
- 변수를 초기화할 때의 값에 따라 타입이 결정 
- 타입이 결정되면 같은 타입으로만 수정 가능
- dart에서 주로 사용이 권장됨


## 명시적 타입
- int, double, String 등 직접적으로 타입을 명시해서 사용
- class의 property를 작성할 때 권장


## Dynamic
- 여러타입을 가지는 변수 또는 어떤 타입을 가지는지 모르는 상황에서 사용
- 주로 json 등의 데이터 처리 시 사용됨 
- 유용하나 안정성을 위해 사용이 권장되지 않음 


## Null Safety
- 개발자가 null값을 참조할 수 없도록 하는 것 
- 기본적으로 Dart의 모든 변수는 non-nullable 상태
- null 값이 사용되면 런타입 에러를 발생시키기에 주의해야 함
- null 값을 사용하고 싶으면 사용할 변수의 타입에 '?'를 붙여 명시적으로 알림   
  *String? => '이 변수는 String일 수도 있고, null일 수도 있다'라는 의미*
- ? 를 사용하면 해당 변수가 null값이 아니라는 것을 확인하기 위해 null-check를 해야 한다
  ```dart
  void main() {
	  String? name = 'name';
	  name = null;
	  
	  String title = 'title';
	  title = null; // title 변수는 non-nullable 상태라 오류가 발생 
	  if(name != null) {
		  name.isNotEmpty; // name이 null이 아니면 실행 
	  }
	  title?.isNotEmpty; // 위의 if문과 같은 동작을 하는 코드
	  // 여기서 ?는 isNotNull의 의미
  } 
  ```


## Final
- 수정이 불가능한 변수를 생성 
	```dart
	final name = 'name';
	name = 'name2'; // 에러 발생 

	final String title = 'title'; // 구체적으로 타입을 명시해줄 수 있음
	```   
- 이 타입의 변수는 한번 초기화되면 수정할 수 없음 
- const 와 비슷하지만 사용차이가 있음 (final)
- 런타임중에 만들어질 수 있음 


## Last
- final 이나 var 앞에 붙여주는 수식어
- 초기 데이터 없이 변수을 선언할 수 있도록 해줌 
```dart
late final name; // 가능
final title ; // 불가능

name = 'name'; // 나중에 선언해도 final 변수라 선언이후 수정이 불가능
```   


## Constant
- 상수
- compile-time constant 
- final과 비슷하게 선언후 수정할 수 없음 
- late와 함께 사용할 수 없음
- ==compile_time에 알고있는 값만 사용가능==
- Api에 요청한 값처럼 컴파일 이후에 받아오는 값에는 const를 사용할 수 없음 
```dart
const apiKey = 'aaaddd1123'; // 문제 없음
const UserId = getUserData(); // 사용할 수 없음 
final UserData = getUserData(); // 문제 없음
late const password = '*****'; // late와 const를 같이 사용할 수 없음

// const = 앱이 실행되기 전 부터 정해져있는/알고있는 값
// final = 컴파일 이후에 입력되는/받아오는 값 
```
<br>


----
#Dart #variable #var #dynamic #null-safety #final #const #last

[[home\|home]]