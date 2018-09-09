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