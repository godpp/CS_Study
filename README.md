# # iOS 공부


## # App Life Cycle

iOS에서 앱은 간단하게 3 가지 실행 모드와 5 가지의 상태로 구분이 가능하며 항상 하나의 상태를 가지고 있습니다.

* Not Running
	* 실행되지 않는 모드와 상태를 모두 의미합니다.
* Foreground
	* Active
	* Inactive
* Background
	* Running
	* Suspend

* Not Running -> Active
	* 앱을 터치해서 실행이 되는 상태입니다.
* Active -> Inactive -> Running
	* 앱을 활성화 상태에서 비활성화 상태로 만든 뒤, 백그라운드에서도 계속 실행중인 상태입니다.
* Active -> Inactive -> Suspend
	* 앱을 활성화 상태에서 비활성화 상태로 만든 뒤, 백그라운드에서도 정지되어 있는 상태입니다.
* Running -> Active
	* 백그라운드에서 실행 중인 앱이 다시 Foreground에서 활성화 되는 상태입니다.


## # View Life Cycle

* viewDidLoad
	* 뷰 컨트롤러 클래스가 생성될 때, 가장 먼저 실행됩니다. 특별한 경우가 아니라면 딱 한 번 실행되기 때문에 초기화 할 때 사용 할 수 있습니다.
* viewWillAppear
	* 뷰가 생성되기 직전에 항상 실행이 되기 때문에 뷰가 나타나기 전에 실행해야 하는 작업들을 여기서 할 수 있습니다.
* viewDidAppear
	* 뷰가 생성되고 난 뒤에 실행 됩니다. 데이터를 받아서 화면에 뿌려주거나 애니메이션 등의 작업을 하는 로직을 위치시킬수 있습니다. (viewWillAppear에 로직 넣었다가 뷰에 반영이 안되는 경우가 있음.)
* viewWillDisappear
	* 뷰가 사라지기 직전에 실행 됩니다.
* viewDidDisappear
	* 뷰가 사라지고 난 뒤에 실행 됩니다.


## # Enum, Struct, Class

> Enum (열거형)

* 변수가 가질 수 있는 가능한 값들을 나열해 놓은 타입
* 값의 종류가 일정한 범위로 정해 있을 때 쓰는 것이 편리

```
enum Compass {
	case North
	case South
	case East
	case West
}

var directionToSeoul : Compass
directionToSeoul = Compass.west
directionToSeoul = .North
```

> Struct(구조체)와 Class(클래스)

* Struct(구조체)
	* 서로 다른 자료형의 변수들을 묶어 하나의 새로운 자료형을 만들 수 있으며, 이 새로운 자료형을 구조체라고 한다. (값 타입)
* Class(클래스)
	* 클래스는 구조체와 같이 서로 다른 자료형의 속성과 메소드를 포함한다. 상속을 통해 자식 클래스에 자신의 속성과 메소드를 물려줄 수 있다. (참조 타입)
* 값 타입
	* 스택 영역에 저장되며 선언되는 즉시 메모리 할당
	* 하나를 선언할 때 마다 하나의 공간을 가짐
```
struct S {
	var data: Int = -1
}
var a = S()
var b = a
a.data = 42
print("\(a.data), \(b.data)") // "42, -1"
```


* 참조 타입
	* 힙 영역에 저장되며 스택에서는 주소 값만 가지고 있는 형식
```
class C {
	var data: Int = -1
}
var x = C()
var y = x
x.data = 42
print("\(x.data), \(y.data)") // "42, 42"
```

* Class와 Struct의 유사성
	* 값을 저장할 속성을 정의한다.
	* 기능을 위한 메소드를 정의한다.
	* 초기상태를 설정하기 위한 init이라는 초기설정자를 제공한다.
	* 기본 구현내용을 확장하기 위한 기능 제공 (extension)
* Class와 Struct의 차이점
	* 클래스는 구조체가 가지지 못한 다음 기능을 가진다.
		* 부모 클래스의 특성을 상속받는 기능이 가능
		* 클래스 인스턴스 형을 검사하고 반영하여 런타임시에 형변환을 할 수 있다.
		* 할당된 임의의 리소스를 헤제하는 deinitializer를 가진다.
		* 클래스 인스턴스는 참조 카운터를 하나 이상 허용한다.


## # Protocol (프로토콜)

* 프로토콜은 메소드, 속성 그리고 다른 특정 작업 또는 기능의 부분에 맞는 요구 사항을 정의 (구현은 하지 않음).
* 프로토콜은 요구사항의 실제 구현을 제공하기 위한 Class, Struct, Enum에 적용한다.

```
protocol Sendable {
	var from: String? { get }
	var to: String { get }

	func send()
}

struct Mail: Sendable {
	var from: String?
	var to: String

	func send() {
		print("Send a mail from \(self.from) to \(self.to)")
	}
}

struct Feedback: Sendable {
	var from: String? {
		return nil // 피드백은 무조건 익명으로 보낸다.
	}

	var to: String

	func send() {
		print("Send a feedback to \(self.to)")
	}
}

//MARK: 프로토콜은 마치 추상클래스처럼 사용 가능
func sendAnything(_ sendable: Sendable) {
	sendable.send()
}

let mail = Mail(from: "taylored@naver.com", to: "talentx076@gmail.com")
sendAnything(mail)

let feedback = Feedback(from: talentx076@gmail.com)
sendAnything(feedback)
```














	