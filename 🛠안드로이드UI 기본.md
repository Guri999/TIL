Android UI - Widget
=
# 🛠안드로이드UI 기본

## 👷**UI(UserInteface)설계 개요**

### 뷰(View)의 구성

1. **위젯(Widget)**
    - View의 서브 클래스로서, 앱 화면을 구성하는 시각적인 모양을 지닌 UI요소
    - 예) 버튼,메뉴,리스트 등
2. **레이아웃(Layout)**
    - ViewGroup의 서브 클래스로서, 다른 뷰(위젯 혹은 레이아웃)를 포함하면서
    이들을 정렬하는 기능을 지닌 UI요소
    ## 👷**UI 설계 방법**

### 01. XML을 사용하여 UI설계

### AndroidStudio의 Layout Editor이용

- 드래그 앤 드롭 방식의 WYSIWYG(what you see is what you get) 에디터
- 다양한 디바이스 / 안드로이드 버전에 대한 Preview
- XML코드 자동 변환 및 동기화
### Layout Editor

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/05f8e160-4718-4b42-ba27-5f73df4aacbd/Untitled.png)

### 1) Palette

- 레이아웃으로 드래그 할 수 있는 다양한 뷰 및 뷰 그룹을 포함합니다.

### 2) Component Tree

- 레이아웃에서 구성요소의 계층 구조를 표시합니다.

### 3) 툴바

- 편집기에서 레이아웃 모양을 구성하고 레이아웃 속성을 변경하려면 이 버튼을 클릭합니다.

### 4) 디자인 편집기

- 디자인 뷰나 청사진 뷰 또는 두 뷰 모두에서 레이아웃을 수정합니다

### 5) Attributes

- 선택한 뷰의 속성을 제어할 수 있는 영역입니다

### 6) 뷰 모드

- 레이아웃을 코드, 디자인, 분할 모드 중 하나로 표시합니다.
- 분할 모드는 코드 창과 디자인 창을 동시에 표시합니다.

### 7) 확대/축소 및 화면 이동 컨트롤

- 편집기 내에서 미리보기의 크기와 위치를 제어합니다.

## 2. 📱위젯(Widget)

### 2.1 위젯이란?

### ❓위젯(Wdiget)는 과연 무엇일까?

- View의 서브 클래스 중에서 화면에 보이는 것들을 말함
- 대표적인 위젯은 TextView, EditText, Button등이 있습니다.

# 2. 📱위젯(Widget)

### 2.1 위젯이란?

### ❓위젯(Wdiget)는 과연 무엇일까?

- View의 서브 클래스 중에서 화면에 보이는 것들을 말함
- 대표적인 위젯은 TextView, EditText, Button등이 있습니다.
# 2. 📱위젯(Widget)

### 2.1 위젯이란?

### ❓위젯(Wdiget)는 과연 무엇일까?

- View의 서브 클래스 중에서 화면에 보이는 것들을 말함
- 대표적인 위젯은 TextView, EditText, Button등이 있습니다.

### View

### 01. ❓View란 무엇일까?

- View클래스는 모든 UI 컴포넌트들의 부모 클래스
- View클래스의 속성은 모든 UI컴포넌트들에서 공통적으로 사용 할 수 있다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/116e9176-fecc-43ec-a5ea-b3359a045770/Untitled.png)

### 02. layout_width, layout_height

- **match_parent(혹은fill_parent)** : 부모 UI컴포넌트의 크기에 맞춤
    - SDK2.2(프로요)부터는 match_parent로 변경. 둘다 사용 가능
- **wrap_content** : UI컴포넌트의 내용물 크기에 맞춤

### 03. 다양한 스마트폰 해상도 대응 방법

### 안드로이드DP(Dip),PX,DPI의 개념

px등으로 크기를 정해주면 사이즈가 기기마다 전 부 똑같이 되서 유동적인 dp를 써줌

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/faa520eb-9ffa-455f-ad35-4f2ae9c92ddd/Untitled.png)

### 1) 스크린의 실제 단위 → px

- PX단위는 화면의 전체 화면 크기와 상관 없이 지정한 수치만큼 표시되는 절대적     표시 단위

### 2) dp(Density-independentPixel)

- 밀도 또는 독립 화소를 말하며, 디스플레이의 해상도(밀도)와 상관 없이 다룰 수 있는단위

### 3) dpi(dotsperinch)

- DPI는 DotPerInch로 1인치에 들어가는 픽셀을 나타내는 단위이다.
- 예를 들면 100DPI는 1인치 당 픽셀이 100개 포함 된다는 것을 말한다.
- 개수가 많을수록 고밀도이며 안드로이드에서 주요DPI는 아래와 같다

### TextView

### 실제 디바이스에서 실행시켜보자

- **화면에 text를 표시 하는 용도**
- **주요 속성**
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6f38c396-3394-40dc-9d0b-e3991fbe4011/Untitled.png)
    

### 2.4 EditText

### 입력이 가능한 Text창

### 주요 속성

- TextView의 모든 속성 상속(EditText는TextView의 서브클래스임)
- inputType: 입력 시 허용되는 키보드 타입 설정 및 키보드 행위를 설정
    
    ### 키보드 타입 설정 값
    
    - “text”:일반적인 텍스트 키보드
    - “phone”:전화번호 입력 키보드
    - “textEmailAddress”:@문자를 가진 텍스트 키보드
    
    ### 키보드 행위 설정 값
    
    - “textCapWords” : 문장의 시작을 대문자로 변환
    - “textAutoCorrect” : 입력된 단어와 유사한 단어를 제시하고 제시된 단어 선택 시,입력된 단어를 대치
    - “textMultiLine”:여러 줄을 입력 받을 수 있음

    📁 ImageView