# Dart - language

## Environment
- [DartPad](https://dartpad.dartlang.org/)

## 주요 컨셉
- Reference. [Important concepts from Dart documents](https://www.dartlang.org/guides/language/language-tour#important-concepts)

1. 변수에 대입할 수 있는 것들은 모두 객체이다. 모든 객체는 `class`의 인스턴스로 `Object` 클래스로부터 상속받으며, `숫자`, `함수`, `null`은 모두 객체이다.
2. `Dart`는 강타입 언어이지만, 타입 명시를 따로 하지 않아도 된다.  `Dart`가 타입을 유추할 수 있기 때문이다. 다만, 명시적으로 타입이 지정되지 않았다고 코드를 작성해야 하는 경우는 `dynamic` 타입을 사용한다.
3. `Dart`는 제네릭 타입을 지원한다. (예. `List<int>`, `List<dynamic>`)
4. `Dart`는 클래스 혹은 객체에 연결된 함수 뿐만 아니라, 최상위 함수도 지원한다. 또한, 자바스크립트처럼 함수 내에 함수를 중첩하여 만들 수 있다.
5. `Dart`는 클래스 또는 객체에 연결된 변수(정적 변수 및 인스턴스 변수)뿐만 아니라, 최상위 변수도 지원한다. 이 때, 인스턴스 변수는 필드 또는 프로퍼티라고 한다.
6. `Dart`는 `Java`와 달리 `public`, `protected`, `private` 등의 키워드가 없으며, `_`로 시작하는 식별자는 비공개이다.
7. 식별자는 숫자, 문자 및 `_`로 이루어지며, 문자 또는 `_`로 시작할 수 있다.
8. 무언가가 표현식(expression)인지 명령문(statement)인지 여부는 중요하며, 두 단어에 대해 정확해야 한다. (무슨 말인지 제대로 이해하지 못했음)
9. `Dart` 툴은 두 종류(warnings, errors)의 문제를 리포팅할 수 있다.  워닝은 코드가 작동하지 않을 수도 있지만, 프로그램의 실행을 방해하지는 않는다.  에러는 컴파일 타임 또는 런타임에 발생하며, 컴파일 타임 에러는 프로그램이 실행되지 않게 하며, 런타임 에러는 프로그램이 실행되는 동안 예외가 발생하게 된다.

## Comment
```dart
// this is a comment.

/**
 * This is a multi-line comment.
 * It must be started with /* and end with */
 */
```

## Primitive type
```dart
// boolean
bool thisIsTrue = true;
bool thisisFalse = false;

// number
int num = 42;
int hexNum = 0xabcd;

double float = 0.3;
double exponent = 1.42e5;

// string
String s = 'string';
/* ${expression} can be skipped the {} */
String quote = '$s with quotation.'; // string with quotation.
String doubleQuote = "${s} with double quotation."; // string with double quotation.

String concatenation = 'String '
  'concatenation'
  " is so simple.";

String stringPlusString = 'string ' + 'will be concatenated.';

String multilineString = '''
Hello,
World!
''';

// Non-specitying variables
var varNum = 42;
var varStr = 'Hello';

dynamic dynamicValue = 'It can be any type';

// list
final mutableList = [4, 2, 3];
mutableList[0] = 3; // [4, 2, 3]

final immutableList = const [1, 2, 3];
immutableList[0] = 4; // throw errors

// map
const dictionary = { // keys and values can be any type of object.
  'a': 1,
  '2': 2,
  2: 3, // keys can not be dulplicated. but, '2' and 2 is different.
  true: 4,
  {}: 5,
};

const instanceOfMap = Map();
instanceOfMap['key'] = 'value';
instanceOfMap['undefinedKeyName']; // null

dictionary.length; // 5

var immutableValue = const {
  'hello': 'world'
};
immutableValue['hello'] = 'dart'; // hthrow errors

// rune
var clapping = '\u{1f44f}';
print(clapping); // 👏

Runes runeClapping = new Runes('\u{1f44f}');
print(runeClapping); // (128079)
print(new String.fromCharCodes(runeClapping)); // 👏

// symbol
print(#hello); // Symbol('#hello');
```

### Floating point issue
```dart
// 0.1 + 0.2 = 0.3 ?
double a = 0.1;
double b = 0.2;
print(a + b); // 0.30000000000000004
```

### dynamic
```dart
var a = 42;
a = 5;
a = 'Hello'; // throw errors

dynamic b = 'I'm String';
b = 0;
b = true;
```

### Default value
```dart
var uninitialized;
print(uninitialized); // null
```

## Constants
변수를 변경하지 않는다면, `var`대신 `const`를 사용하거나 타입 앞에 `final`을 사용한다. `const`는 컴파일 타임 상수로 암시적으로는 `final`변수와 같다. `final` 변수(최상위 레벨 변수 또는 클래스 변수)는 처음 사용될 때 초기화된다.
```dart
final a = 42;
final int num = 5;
```

## Functions
`Dart`의 함수는 객체로 `Function`타입이다. `JavaScript`의 함수와 마찬가지로 변수에 할당되거나 반환될 수 있으며, 다른 함수의 인자로 전달될 수도 있다. 또한, 함수는 익명일 수도 있다.
```dart
add(int a) {
  return (int b) {
    return a + b;
  };
}

// arrow function
// add(int a) => (int b) => (a + b);

final addTwo = add(2);

const list = [1, 2, 3];

final newList = list.map(addTwo);

print(newList); // 3, 4, 5
```

### 파라미터
파라미터는 몇 번째 인자인지에 따라 구분되거나, 전달된 인자의 이름에 따라 구분될 수 있다.
```dart
// named parameters
move(meter: 10, direction: 'ease');
void move({ int meter, String direction }) { /* ... */ }

// positional parameters
moveTo('Seoul', 'Busan');
void moveTo(String from, String to) { /* ... */ }
```

#### 선택적 기명 파라미터
- 함수 호출 시 `선택적 기명 파라미터`를 사용하기 위한 문법은 다음과 같다.
```dart
paramName: value
```
- 함수 정의 시 `선택적 기명 파라미터`를 사용하기 위한 문법은 다음과 같다.
```dart
returnType functionName({ paramType paramName }) { /* ... */ }
```
- 반드시 전달되어야 하는 인자를 사용하기 위해서는 `@required`를 사용한다.
  - `@required`는 [meta](https://pub.dartlang.org/packages/meta)에 정의되어 있다.
```dart
// code from dart docs (https://www.dartlang.org/guides/language/language-tour#functions)
const Scrollbar({ Key key, @required Widget child })
```

#### 선택적 위치 파라미터
- 함수 정의 시 `선택적 위치 파라미터`를 사용하기 위한 문법은 다음과 같다.
```dart
String say(String from, String msg, [String device]) {
  final String paragraph = '$from says $msg';

  if (device != null) {
    return '$paragraph with a $device';
  }

  return paragraph;
}
```

#### 기본 매개변수
`JavaScript` `ES2015`의 기본 매개변수와 사용 방법이 거의 동일하다.<br />
하지만, 주의해야할 점이 있다면, 위치 파라미터로써 함수를 정의할 때, 파라미터가 `필수적`이지 않으므로, 기본 매개변수를 사용하는 파라미터는 `선택적 위치 파라미터`로써 정의되어야 한다.
```dart
dynamic add([int a = 2]) => (int b) => (a + b);

final dynamic addTwo = add();
```

### main()
최상위 레벨의 함수로 모든 애플리케이션은 `main`함수를 가지게 된다.<br /> `main`은 애플리케이션의 진입점이며, `void`를 반환하며, 선택적 위치 파리미터 `List <String>` 인자를 전달받을 수 있다.

### 렉시컬 스코프
```dart
bool topLevel = true;

void main() {
  var insideMain = true;

  void myFunction() {
    var insideFunction = true;

    void nestedFunction() {
      var insideNestedFunction = true;

      print(topLevel); // true
      print(insideMain); // true
      print(insideFunction); // true
      print(insideNestedFunction); // true
    }

    nestedFunction();
  }

  myFunction();
}
```

### 클로저
간단하게 말하면
> 클로저는 다른 함수의 스코프 안에 있는 변수들에 접근할 수 있는 함수
라고 할 수 있다.<br />
위에서 사용된 `addTwo`도 `add`의 `a`를 기억하는 클로저이다.

자세한 내용은 (자바스크립트 클로저에 대해 다룬 글이지만) [클로저에 대한 글](https://wonism.github.io/closure)의 내용을 참조바란다.

### 반환 값
모든 함수는 값을 반환하며, 명시적으로 반환되는 값이 없을 경우엔 암묵적으로 `null`이 반환된다.

## 연산자
(일반적인 기본 연산자는 다루지 않는다.)

### 조건 표현식
```dart
String playerName([String name]) => name ?? 'Guest';
print(playerName()); // Guest
```

### Cascade 표현식
`..`를 통해 `JavaScript` 체이닝 패턴과 유사하게 사용할 수 있다.
```dart
querySelector('#confirm') // Get an object.
  ..text = 'Confirm' // Use its members.
  ..classes.add('important')
  ..onClick.listen((e) => window.alert('Confirmed!'));

var button = querySelector('#confirm');
button.text = 'Confirm';
button.classes.add('important');
button.onClick.listen((e) => window.alert('Confirmed!'));
```

### 조건적 멤버 엑세스
표현식은 `?.`이며, `foo?.bar`와 같이 사용한다.<br />
`Ruby`의 `try` 혹은 `&.`와 유사하다.
