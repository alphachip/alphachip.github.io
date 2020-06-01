---
layout: article
title: iOS 앱 개발 입문, 개발 문서로 시작하기
tags: [iOS]
aside:
  toc: true
---
[Start Developing iOS Apps (Swift) : iOS 앱 개발 입문자를 위한 공식 문서](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/index.html#//apple_ref/doc/uid/TP40015214-CH2-SW1)

위 링크의 공식 문서가 영어로 되어 있어서 다음에 내용을 빨리 복습하기 위해 기록으로 남깁니다.

# Getting Started
## Jump Right In
### Prerequisites : 전제조건
스위프트 프로그래밍 언어와 친근하다고 가정한다. 마스터할 필요는 없지만 편안히 읽을 수 있고 이해할 수 있다면 더욱 많이 얻을 것이다(참고로 저(지금 한글로 글을 작성중인 본인)는 스위프트는 접한 적 없지만 C, C++, Java를 어느 정도 다룰 줄 알고 Python을 능숙하게 다루진 못해도 기본 문법을 알고 있고, 안드로이드 스튜디오 프로젝트를 몇 개 만든 적 있습니다).

아직 스위프트가 편하지 않다면 [스위프트 플레이 그라운드 앱(Swift playgrounds app)](https://apps.apple.com/us/app/swift-playgrounds/id908519492)을 설치해서 익히면 된다는데... iPad밖에 안되는 모양이네요 :question::exclamation::rage::rage::rage::anger::punch:

### About the Lessons
이번 레슨들에서는 간단하게 'FoodTracker' 앱을 만들게 될 겁니다. 음식 목록을 보여주는데, 각 음식에의 이름, 평점, 사진을 설정할 수 있고 사용자는 목록에서 음식을 추가, 삭제, 수정이 가능합니다. 추가나 수정을 할 때는 다른 화면으로 이동해서 구체적인 이름, 평점, 사진을 지정할 수 있습니다.

각 레슨의 마지막에 코드와 인터페이스가 어떻게 보여야 하는지를 보여주는 Xcode 프로젝트 파일이 제공됩니다.

레슨에서 개념을 참고해야할 때 기존의 기억 대신에 용어집(Glossary)에 있는 것들로 기억하세요. 용어집은 수업 전체에 연결됩니다.

### Get the Tools
이 레슨들에 설명된 최신 기술을 사용해 앱을 개발하려면 맥OS 10.11.5 이상으로 최신 버전 Xcode를 실행해야합니다. Xcode에는 모든 기능(디자인, 개발, 앱 디버깅)이 포함되어있습니다. 또, iOS 개발을 위해 툴, 컴파일러,프레임워크가 가능한 SDK가 포함되어 있습니다.

App Store에서 최신 Xcode를 다운받으세요. 다운받은 Xcode를 Applications 파일에 넣어주면 됩니다.

레슨들은 Xcode 8.1, iOS SDK 10, Swift 3을 사용하여 작성되었습니다.

# Building the UI
## Build a Basic UI
간단히 'FoodTracker' 앱을 만들 것입니다. 앱 내에는 음식 이름(Meal Name) 라벨(label), 음식 이름을 바꾸기 위한 텍스트 필드(text field, 글자 입력 가능한 칸), 이름을 재설정하기 위한 버튼을 만들 것입니다.

### Learning Objectives
이번 레슨을 통해 배우는 것을 요약하자면 Xcode 프로젝트 내의 스토리보드(Storyboard)에서 UI(User Interface)를 다루고 실행시키기입니다.

### Create a New Project
Xcode 템플릿에는 일반 iOS 앱(탭 기반(tab-based) 탐색/테이블 기반(table-based, 이건 아마 타임라인처럼 목록형을 뜻하는 것 같습니다)), 게임을 제공하는데 대부분 인터페이스와 소스 코드가 포함되어 있습니다.

Create a new Xcode Project(혹은 File>New>Project)>iOS탭>Single View Application>Next버튼

Project option에서 추가 사항을 입력:
* Product Name: FoodTracker
* Team: 없으면 None
* Organization Name: 조직 이름이나 내 이름이나 빈칸도 됨
* Organization Identifier: 조직을 식별할 수 있는 걸로 적기. 디폴트(default) 값은 `com.example.`로 설정되는데 디폴트 값으로 두면 앱스토어에 못 올린다고 어디선가 봤던 것 같습니다.
* Bundle Identifier: product name과 Organization Identifier로 자동으로 생성. 적는 공간이 아닙니다.
* Language: swift
* Devices(최신 버전에서는 프로젝트 생성 후에 General 설정에서 선택 가능): Universal(iPhone과 iPad 둘 다를 의미)
* User Interface(최신 버전에 있음): Storyboard
* Use Core Data: 선택 안 함
* Include Unit Tests: 선택함
* Include UI Tests: 선택 안 함

최신 버전에는 User Interface이라고 Swift UI와 Storyboard 항목이 있고 Storyboard가 기본 선택이 되어 있습니다. 찾아보니 Storyboard의 단점을 보완한 것이 Swift UI라고 합니다. 하지만 제한된 API 영역, SDK(iOS13, macOS 10.15, tvOS 13, watchOS 6이상), 지원(기존에 쓰이던 UIKit는 10년 이상 지원되어왔음)이라는 신생의 단점?이 있습니다.

하지만 Swift UI가 추후에 대체될 것임은 예견된 일인데다 실무까지 고려한다면 우선 Storyboard로 익히고 Swift UI도 알아가는 것이 좋을 것으로 생각합니다(이 레슨에서도 Storyboard 기준인 듯 하니까요).

Next 클릭

FoodTracker에 서명하려면 개발팀이 요구된다는 에러 아이콘의 메시지를 보더라도 시뮬레이터에 앱을 돌리기 위해서는 필요하지 않기 때문에 이 레슨을 끝내는 데에는 문제가 되지 않습니다.

하지만 iOS 기기에 직접 돌리려면 서명이 필요합니다. 애플 개발자 프로그램에서 개인 혹은 조직의 멤버의 팀을 선택할 수 있는데 그렇지 않으면 Apple ID가 개인 팀으로 할당합니다. 앱 스토어에 앱을 올리려면 애플 개발 프로그램에 가입해야 합니다. 더 많은 안내는 Help>Xcode Help>Signing workflow 검색

### Get Familiar with Xcode
Xcode는 앱 개발을 위한 모든 파일과 리소스로 구성됩니다. 그리고 코드와 UI를 위한 편집과 빌드, 실행, 디버그를 제공합니다.

화면은 Navigator area(파일 접근), Editor area(코드/UI/리소스 편집), Utility area(선택된 것의 정보. 윗 부분은 정보를 보고 편집할 수 있는 inspector pane, 아래 부분은 UI요소, 게임 매크로의 역할을 하는 코드 조각(Code Snippet), 다른 리소스들에 접근할 수 있는 library pane), Toolbar(빌드와 실행, 실행의 진행 과정 표시, 작업 환경 설정) 창으로 나뉩니다.

### Run iOS Simulator
Toolbar에서 기기를 iPhone7으로 설정합니다(저는 실제 기기로 했는데 그닥 어렵지 않았던 것 같습니다).

그 후 Toolbar의 삼각형 모양의 Run버튼 혹은 Product>Run 혹은 Command-R키를 클릭하여 실행합니다.

실행을 누르면 개발 모드 허용할 지 묻는 창이 뜰 수 있는데 허용해놓으면 디버깅할 때마다 비밀번호를 묻지 않습니다.

처음에는 시작할 때 몇 분 걸릴 수 있습니다.

실행된 화면에는 그냥 하얀 화면이 뜰 겁니다. 다른 템플릿을 선택했다면 더 복잡한 행위를 할 거구요.

Simulator>Quit Simulator 혹은 Command-Q로 시뮬레이터를 종료합니다.

### Review the Source Code
Single View Application 템플릿에는 앱 환경을 설정하는 몇 개의 코드 파일이 있습니다.
1. AppDelegate.swift (직역하면 앱 대리자)
Navigator area에서 Navigator Selector bar(선택할 수 있는 아이콘 모여있는 곳)에서 Project Navigator(파일모양. 안보이면 맨 왼쪽 버튼) 버튼을 선택. 혹은 View>Navigators>Show Project Navigator.

여기서는 폴더 목록 옆의 삼각형으로 폴더 탐색이 가능합니다다.

FoodTracker 파일 안의 AppDelegate.swift를 선택하면 Editor area에서 소스 코드를 볼 수 있습니다.

AppDelegate.swift에는 두 가지 기본 기능이 있습니다.
* AppDelegate 클래스 정의하기. 이 클래스는 앱 콘텐츠가 그려지는 창을 만들고 앱 내의 상태 전환을 반응할 공간을 제공합니다.
* entry point(제어가 들어가는 프로그램이나 부분코드)를 생성하고 run loop(작업을 예약하고 event가 들어올 때 이를 조정하는 event 처리 루프)이 input event를 앱에 전달합니다. 이 작업은 UIApplicationMain 속성이 합니다(맨 위 코드에 위치함).

UIApplicationMain 속성을 사용하는 것은 UIApplicationMain 함수를 불러 AppDelegate 클래스를 대리자 클래스 이름으로 보내는 것과 같습니다.

응답으로는 시스템이 Application object(life cycle을 관리함)를 생성합니다. 또한 AppDelegate 클래스의 instance를 만들어 Application object에 할당합니다.

그리고 시스템이 앱을 시작합니다.

AppDelegate 클래스는 새 프로젝트를 만들 때마다 자동으로 생성됩니다. 아주 이례적인 상황이 아니라면 앱 초기화와 앱단의 이벤트에 반응하기 위해 Xcode에서 제공하는 것으로 사용하는 것이 좋습니다. 그리고 AppDelegate 클래스는 UIApplicationDelegate 프로토콜을 채택합니다. 이 포로토콜은 앱을 설정, 앱 상태 변화에 반응, 다른 앱단 이벤트를 처리를 위해 사용하는 여러 메소드를 정의합니다.

AppDelegate 클래스는 window라는 single property를 포함합니다.
```swift
var window: UIWindow?
```

이 속성은 앱 윈도우에 대한 참조를 저장합니다. 이 윈도우는 앱의 뷰 계층의 루트를 나타냅니다. 따라서 앱의 모든 내용이 그려집니다. 윈도우 속성은 optional(값이 nil(값이 없음을 뜻함)일 수 있음).

AppDelegate 클래스는 stub(stub 함수: 함수가 구현되지 않았거나 라이브러리에서 제공하는 함수거나 반환값을 임의로 생성하기 위함의 목적이거나 테스트 단순화 목적으로 사용) 구현도 포함돼있다.

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool
func applicationWillResignActive(_ application: UIApplication)
func applicationDidEnterBackground(_ application: UIApplication)
func applicationWillEnterForeground(_ application: UIApplication)
func applicationDidBecomeActive(_ application: UIApplication)
func applicationWillTerminate(_ application: UIApplication)
```






### Open Your Storyboard
### Build the Basic UI
### Preview Your Interface
### Adopt Auto Layout
### Debugging Auto layout
### Wrapping Up

## Connect the UI to Code
### Learning Objectives
### Connect the UI to Source Code
### Process User Input
### Wrapping Up

## Work with View Controllers
### Learning Objectives
### Understand the View Controller Lifecycle
### Add a Meal Photo
### Display a Default Photo
### Connect the Image View to Code
### Create a Gesture Recognizer
### Connect the Gesture Recognizer to Code
### Create an Image Picker to Respond to User Taps

## Implement a Custom Control
### Learning Objectives
### Create a Custom View
### Display the Custom View
### Add Buttons to the View
### Add Support for Interface Builder
### Add Star Images to the Buttons
### Implement the Button Action
### Add Accessibility Information
### Connect the Rating Control to the View Controller
### Clean Up the Project
### Wrapping Up

## Define Your Data Model
### Learning Objectives
### Create a Data Model
### Test Your Data
### Wrapping Up

# Working with Table Views
## Create a Table View
### Learning Objectives
### Create the Meal List
### Design Custom Table Cells
### Add Images to Your Project
### Connect the Table Cell UI to Code
### Load Initial Data
### Display the Data
### Prepare the Meal Detail Scene for Navigation
### Wrapping Up

## Implement Navigation
### Learning Objectives
### Add a Segue to Navigate Forward
### Configure the Navigation Bar for the Scenes
### Store New Meals in the Meal List
### Create an Unwind Segue
### Disable Saving When the User Doesn't Enter an Item Name
### Cancel a New Meal Addition
### Wrapping Up

## Implement Edit and Delete Behavior
### Learning Objectives
### Enable Editing of Existing Meals
### Cancel an Edit to an Existing Meal
### Support Deleting Meals
### Wrapping Up

## Persist Data
### Learning Objectives
### Save and Load the Meal
### Save and Load the Meal List
### Wrapping Up

# What's Next?
## Where to Go from Here

# iOS and Swift Terminology
## Glossary
문서 내의 용어를 설명 해놓은 곳입니다.

# Revision History
## Document Revision History
이 항목은 문서가 변경되었을 때 날짜와 관련 내용을 메모해놓은 것입니다.
