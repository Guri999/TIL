프래그먼트 (Fragment)
=
그게머임?
->
### 01. ❓과연 프래그먼트(Fragment)은 무엇일까?

- **액티비티 위에서 동작하는 모듈화된 사용자 인터페이스**
    - **액티비티와 분리되어 독립적으로 동작할 수 없음**
- **여러 개의 프래그먼트를 하나의 액티비티에 조합하여 창이 여러 개인UI를 구축할 수 있으며,하나의 프래그먼트를 여러 액티비티에서 재 사용할 수 있음**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2c4244ab-fa01-4899-85ed-41f29f12ff94/Untitled.png)

하나의 액티비티 화면 내에서 특정 영역만 교체하는거

### 02. 🤗 프래그먼트 예

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3bc649ac-a2b4-4876-a28d-64cb2e68c950/Untitled.png)

### 03. 🤗 액티비티 vs 프래그먼트 비교

### 1) Activity
- 시스템의 액티비티 매니저에서 인텐드를 해석해 액티비티간 데이터를 전달
### **2) Fragment**

- **액티비티의 프래그먼트 매니저에서 메소드로 프래그먼트간 데이터를 전달**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bf5ec753-20b0-4ce2-855a-3077e47edb11/Untitled.png)

### 04.  프래그먼트 생명주기
#### **프래그먼트의 주요 생명주기 메서드:**

1. **onAttach()**
    - 프래그먼트가 액티비티에 연결될 때 호출됩니다.
    - 이 시점에서 프래그먼트는 액티비티와 아직 완전히 연결되지는 않았습니다.
2. **onCreate()**
    - 프래그먼트가 생성될 때 호출됩니다.
    - 초기화 작업, 리소스 바인딩 등을 수행할 수 있습니다.
3. **onCreateView()**
    - 프래그먼트의 레이아웃을 인플레이트하는 곳입니다.
    - 뷰를 생성하고, 레이아웃을 설정합니다.
4. **onActivityCreated()**
    - 액티비티의 **`onCreate()`** 메서드가 완료된 후 호출됩니다.
    - 액티비티와 프래그먼트의 뷰가 모두 생성된 상태이므로, 뷰와 관련된 초기화를 수행합니다.
5. **onStart()**
    - 프래그먼트가 사용자에게 보여질 준비가 되었을 때 호출됩니다.
    - 필요한 리소스를 할당하거나, 애니메이션을 시작할 수 있습니다.
6. **onResume()**
    - 프래그먼트가 사용자와 상호작용할 수 있는 상태가 되었을 때 호출됩니다.
    - 프래그먼트가 포그라운드에 있을 때 실행되는 작업을 여기서 처리합니다.
7. **onPause()**
    - 프래그먼트가 일시정지될 때 호출됩니다.
    - 상태 저장, 스레드 중지 등의 작업을 수행합니다.
8. **onStop()**
    - 프래그먼트가 더 이상 사용자에게 보이지 않을 때 호출됩니다.
    - 리소스 해제, 스레드 정지 등을 수행합니다.
9. **onDestroyView()**
    - 프래그먼트의 뷰와 관련된 리소스를 정리할 때 호출됩니다.
10. **onDestroy()**
    - 프래그먼트가 파괴될 때 호출됩니다.
    - 프래그먼트의 상태를 정리하고, 모든 리소스를 해제합니다.
11. **onDetach()**
    - 프래그먼트가 액티비티로부터 분리될 때 호출됩니다.
    - 프래그먼트가 액티비티와의 모든 연결을 해제합니다.

### 05. 🤔프래그먼트는 왜 사용할까?

- **Activity로 화면을 계속 넘기는 것보다는 Fragment로 일부만 바꾸는 것이 자원 이용량이 적어 속도가 빠르기 때문**

### 사용하는 이유가 뭘까?

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7c534f4d-82ac-4c11-9f0e-03d48e88ab74/Untitled.png)

### 06. 🤗 프래그먼트 정의하기
- 액티비티를 만들 때와 비슷하게, 하나의 Kotlin 소스 파일과 하나의 XML레이아웃로 정의



프래그먼트를 액티비티 레이아웃에 추가하는 방법은 크게 2가지가 있음
xml파일안에서 프래그먼트를 직접지정
2번째는 코틀린 코드에서 추가

### 07. 🤗프래그먼트를 액티비티의 레이아웃 파일에 정적 추가하기

- 프래그먼트를 액티비티의 레이아웃 파일 안에서 선언
    - <fragment> 안의 android:name 특성은 레이아웃 안에서 인스턴스화할 Fragment 클래스를 지정
    - [중요] 각 프래그먼트에는 액티비티가 재시작되는 경우 프래그먼트를 복구하기 위해 시스템이 사용할 수 있는 고유한 식별자가 필요합니다. 프래그먼트에 ID를 제공하는 데에는 다음과 같은 세 가지 방법이 있습니다.
        - 고유한 ID와 함께 android:id 속성을 제공합니다.
        - 고유한 문자열과 함께 android:tag 속성을 제공합니다.
        - 위의 두 가지 중 어느 것도 제공하지 않으면, 시스템은 컨테이너 뷰의 ID를 사용합니다.

```kotlin
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/fragment_container"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello World!" />
    <fragment
        android:name="com.skmns.fragmentbasic.FirstFragment"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:id="@+id/fragment" />
</LinearLayout>
```
### 08. 🤗 Kotlin 코드에서 동적으로 프래그먼트 추가하기

```kotlin
supportFragmentManager.commit {
            replace(R.id.frameLayout, frag)
            setReorderingAllowed(true)
            addToBackStack("")
        }
```

- **supportFragmentManager**
    
    사용자 상호작용에 응답해 Fragment를 추가하거나 삭제하는등 작업을 할 수 있게 해주는 매니저
    
- **replace**
    
    어느프레임 레이아웃에 띄울것이냐, 어떤프래그먼트냐
    
- **setReorderingAllowed**
    
    애니메이션과 전환이 올바르게 작동하도록 트랜잭션과 관련된 프래그먼트의 상태 변경을 최적화
    
- addToBackStack
    
    뒤로가기 버튼 클릭시 다음 액션 (이전 fragment로 가거나 앱이 종료되거나)

```kotlin
class MainActivity : AppCompatActivity() {
    private val binding by lazy { ActivityMainBinding.inflate(layoutInflater) }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        binding.apply {
            fragment1Btn.setOnClickListener {
                setFragment(FirstFragment()) // 셋 프래그먼트에 프래그먼트를 파라미터를 줌
            }
            fragment2Btn.setOnClickListener {
                setFragment(SecondFragment())
            }
        }
    }

    //프래그먼트 전환
    private fun setFragment(frag: Fragment) {
        supportFragmentManager.commit {
            replace(R.id.frameLayout, frag) // 프레임 레이아웃에 프래그먼트 뿌리겠다
            setReorderingAllowed(true)
            addToBackStack("")
        }
    }
}
```
