# 뷰 바인딩 (View Binding)

버튼을 클릭하는 이벤트를 주고 싶고 텍스트 뷰를 변경하고싶다

액티비티xml과 코틀린 코드를 연결 해줘야함 그 동안 findViewById써서 액티비티에서 연결해줬음

뷰 바인딩은 findViewById를 안쓰고 다른 걸로 대체

훨신 쉽게 코드를 작성할 수 있다.
### 01. 뷰바인딩 특징
- **뷰 바인딩 기능을 사용하면 뷰와 상호작용하는 코드를 쉽게 작성할 수 있습니다**
- **모듈에서 사용 설정된 뷰 바인딩은 모듈에 있는 각 XML 레이아웃 파일의 결합 클래스를 생성합니다.**
- **바인딩 클래스의 인스턴스에는 상응하는 레이아웃에 ID가 있는 모든 뷰의 직접 참조가 포함됩니다.**
- **대부분의 경우 뷰 바인딩이 findViewById를 대체합니다.**

### 02. 🪢 findViewById와의 차이점

### **1) Null 안전성 (Null Safety)**

뷰 바인딩 기능을 사용하면, 앱이 레이아웃의 각 뷰를 직접 참조할 수 있게 해주는 안전한 코드를 자동으로 생성합니다. 이것은 뷰를 사용할 때 'null' 값으로 인한 오류, 즉 뷰가 아직 화면에 나타나지 않았는데 그 뷰를 사용하려고 할 때 생길 수 있는 문제들을 예방해 줍니다. 

예를 들어, 만약 레이아웃에 버튼이 있어야 하는데 아직 버튼이 생성되지 않았다면, 뷰 바인딩은 이를 안전하게 처리하여 앱이 충돌하지 않도록 합니다. 또한, 만약 레이아웃의 일부만 뷰가 있다면, 뷰 바인딩은 해당 뷰가 '가능성 있는 null'(Nullable)임을 알려주어, 개발자가 더 주의 깊게 코드를 작성하도록 돕습니다.

### **2) 타입 안전성 (Type Safety)**

XML 레이아웃 파일에서 정의된 뷰의 타입과 자동 생성된 바인딩 클래스의 필드 타입이 항상 일치하기 때문에, 타입이 서로 맞지 않아 발생할 수 있는 오류를 방지합니다. 

예를 들어, 이미지 뷰(ImageView)에 텍스트를 설정하려고 하면 오류가 발생할 텐데, 뷰 바인딩을 사용하면 이런 실수를 할 가능성이 없어집니다. 즉, 이미지 뷰는 이미지 뷰로, 텍스트 뷰는 텍스트 뷰로만 사용되게 하여, 잘못된 타입 사용으로 인한 오류가 발생하지 않도록 보장합니다.

### 03. 코틀린에서 뷰바인딩 설정 방법
1) gradle설정
```kotlin
android{
	...
    
    // AndroidStudio 3.6 ~ 4.0
    viewBinding{
    	enabled = true
    }
    
    // AndroidStudio 4.0 ~
    buildFeatures{
    	viewBinding = true
    }
}
```
2)
```kotlin
private lateinit var binding: ActivityMainBinding
    
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        
        binding = ActivityMainBinding.inflate(layoutInflater)
        val view = binding.root
```

```kotlin
private lateinit var binding: ActivityMainBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        binding = ActivityMainBinding.inflate(layoutInflater)
        val view = binding.root

        setContentView(view)

        binding.button1.setOnClickListener {
            binding.textView.text = "바인딩 굿"
        }
    }
```
> **‼️ 중요 ‼️**
> 

뷰 바인딩(View Binding) 기능을 사용할 때, 안드로이드 스튜디오는 레이아웃 파일의 이름을 기반으로 한 바인딩 클래스를 자동으로 생성합니다. 이 클래스는 레이아웃에 있는 모든 뷰에 대한 참조를 포함하며, 이를 통해 코드에서 직접 뷰에 접근할 수 있게 해줍니다. 바인딩 객체의 이름은 레이아웃 파일 이름에 'Binding'을 붙여 만들어집니다.

예를 들어:

- 레이아웃 파일 이름이 **`activity_main.xml`**인 경우, 생성되는 바인딩 클래스의 이름은 **`ActivityMainBinding`**이 됩니다.
- 레이아웃 파일 이름이 **`fragment_home.xml`**인 경우, 생성되는 바인딩 클래스의 이름은 **`FragmentHomeBinding`**이 됩니다.