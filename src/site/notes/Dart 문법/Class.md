---
{"dg-publish":true,"permalink":"/dart/class/"}
---



> Dart는 대부분 class로 이루어져있고, 그만큼 class가 많이 사용됨

```dart
class Player = {
	// class 내부에서는 타입을 명시하는 편이 좋음
	String name = 'tester';
	String type = 'human';
	final int code = 1; // 외부에서 수정불가 
}

void main() {
	// new를 사용할 필요는 없다 
	var player = Player();
	player.name = 'closer'; // 이런식으로 class 내부에 접근 가능
}
```

## Constructors
> class를 사용하기위해 생성할 때 사용하는 생성자 
> 생성자가 값을 받아 class property에 할당해줌
```dart
class Player {
	// class 내부에서는 타입을 명시하는 편이 좋음
	late String name;
	late String type;
	
	Player(String name, String type) {
		this.name;
		this.type;
	}
	// 위의 생산자를 단순화할 수 있음 
	// late제거, 변수에서 type를 지정했기 때문에 생성자에서 따로 알려줄 필요가 없음 
	final String name;
	String type; 
	
	Player(this.name, this.type);
	void greetedOther() {
		print('Hi, $name');
	}
}

void main() {
	var player1 = Player('hero', 'human');
	var player2 = Player('gea', 'dog');
	
}
```


## Name Constructor Parameters
> function에서 사용한것과 같음 

```dart
class Player {
	//String name;
	//String team;
	//String type;
	String name, team, type;
	
	// 위의 변수들은 type이 같아 하나로 합칠 수 있음 
	
	
	// 생성자의 parameter를 중괄호로 감싸주면 됨
	Player({required this.name,required this.team,required this.type});
}

void main() {
	var player = Player(
		name:'park', 
		team: 'blue', 
		type:'human',
	);
}
```

## Named Constructors
```dart
class Player {
	String name; // <= this.name
	String team; // <= this.team
	String type; // <= this.type
	
	Player({
		required this.name,
		required this.team,
		required this.type,
	});
	
	// 생성자의 뒤에 : 를 붙이면 여기서 Player를 초기화하라고 하는것 
	// 
	Player.blueTeamPlayer({
		required String name, 
		required String type,
	}) : this.name = name, 
		 this.type = type, 
		 this.team = 'blue';
	
	Player.redTeamPlayer(String name, String type) 
		: this.name = name, 
		  this.type = type, 
		  this.team = 'red';
}

void main() {
	var bluePlayer = Player.blueTeamPlayer(name:'park', type:'human');
	// 자동으로 team은 blue로 되어있음 
	var redPlayer = Player.redTeamPlayer('hack', 'mecha');
}
```

## Cascade Notation
> 개발자가 알고 사용하면 편리함을 가져다주는 방법
```dart
class Player {
	String name;
	String team;
	String type;
	
	Player({required this.name,required this.team,required this.type});
	
	void greeting() {
		print('Hi, $name');
	}
}

void main() {
	var player = Player(name:'park', team: 'blue', type:'human');
	// player의 내용을 수정하려면 하나하나 해야할까?
	player.name = 'kim';
	player.team = 'red';
	player.type = 'dragon';
	
	// 아래의 코드는 위의 코드와 완전히 같은 동작을 하는 코드이다
	// .. 은 player. 과 같은 의미로 사용된다
	// class를 값으로 가질때 사용이 가능
	var tester = Player(name:'tester', team:'admi', type:'undead')
		..name = 'rich'
		..team = 'poseiken'
		..type = 'undead';
		..greeting();
}
```
## Enums
> 그룹화해서 사용가능한 상수값들을 하나로 묶어서 사용

```dart
// 사용법은 간단하다
enum Team = { red, blue }

class Player {
	String name;
	Team team; // team을 Team 형식으로 변경 
	String type;
	
	Player({required this.name,required this.team,required this.type});
	
	void greeting() {
		print('Hi, $name');
	}
}

void main() {
	var player = Player(name:'park', team: Team.blue, type:'human');
	// team을 입력할때 아무거나 입력이 되는게 아니라 Team 의 안에 있는 red, blue만 가능해짐
	// 실수로 틀리거나, 다른 내용을 입력하면 안될때 유용함 
}
```

## Abstract Classes
> 일종의 청사진, 집은 지어주지만 인테리어는 입주자가 알아서 해야한다 
```dart
abstract class Man {
	void walk(); // 이 메소드의 이름과 반환 타입만 지정해서 정의할 수 있음 
	// 상속 받은 모든 클래스가 특정 메소드를 구현하도록 강제
	// 구현은 필수지만 내용은 알아서
}

class Player extends Man {
	String name;
	double score;
	
	void walk() { // Man class를 상속받았기 때문에 만들어 줘야함
		print('$name is walking');
	}
	void sayHello() {
		print('Hello, $name'); //상속 받지는 않았지만 Player class에서 필요해서 확장
	}
}
```

## Inheritance
> 상속. 한 class가 다른 class를 상속받을 수 있다.
> 상속을 받은 class를 자식, 상속을 한 class를 부모(super)라고 한다.
> 자식 클래스는 부모클래스의 변수, 메소드 등을 사용할 수 있다.

```dart
class Human {
	final String name;
	
	Human(this.name);
	
	void talk() {
		print('hey, Hi');
	}
}
class Man extends Human{
	final int age; 
	
	// 여기서 super는 Human 클래스를 말함 
	// super를 통해서 상위 클래스와 소통(데이터 이동)
	// Human 클래스의 생성자가 named를 사용하면 super(name: name)식으로 작성 
	Man({required this.age, required String name}) : super(name);

	@override
	void talk() {
		super.talk();
		print('bye Guys.');
	}
}

void main() {
	var man = Man(age: 22, name:'park');
	man.talk(); // 부모클래스에서 만들었지만 자식 클래스에게 상속되어 사용 가능 
	
}

```


## Mixins
> 생성자가 _없는_ class 
> with을 사용하여 property와 method를 가져오기만 함
> 여러 class에 재사용이 가능  

```dart
class Run {
	final double speed = 10.11;
}
class Strong {
	int power = 100; 
}
class Warrior with Run, Strong{
	String name;
	Warrior(this.name);
	void whoIsHe() {
    print('His name is $name, He has $power power and $speed speed');
  }
} 
class Knight with Run, Strong{}
class Archer with Run, Strong{}

void main() {
	var warrior = Warrior('chel');
	warrior.whoIsHe();
	// 실행결과 His name is chel, He has 100 power and 10.11 speed
}
```
<br>

---
[[home\|home]]

#Dart 