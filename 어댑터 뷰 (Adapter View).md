# 어댑터 뷰 (Adapter View)

실제 실무에서 많이 쓰는것 : 커스텀 항목 뷰
                          RecyclerView

뷰를 하나만 만들고 재사용해서 쓰겠다

### 1. 어댑터 뷰(AdapterView)개요

### 01.❓과연 어댑터뷰는 무엇일까?

- **어댑터 뷰는 여러개의 항목을 다양한 형식으로 나열하고 선택 할 수 있는 기능을 제공하는뷰**
    - **리스트뷰(ListView)는 항목을 수직으로 나열시키는 방식**
    - **그리드뷰(GridView)는 항목을 격자 형태로 나열시키는 방식**
- **어댑터 뷰는 표시할 항목 데이터를 직접 관리하지 않고,어댑터라는 객체로부터 공급받습니다.**

![](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F540d6db0-01d0-4364-a94b-e5a475cd4a7f%2FUntitled.png?table=block&id=e16d974b-1afe-415f-b4ae-ab6e16cb41b7&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=1790&userId=&cache=v2)

### 02. 어댑터 (Adapter)

- 데이터를 관리하며 데이터 원본과 어댑터뷰(ListView, GridView) 사이의 중계 역할
- 어댑터뷰는 어떻게 데이터 항목을 표시할까요?
    1. 어댑터뷰가 어댑터를 사용하기 위해서는 먼저 데이터 원본이 어댑터에 설정되어야 하고, 어댑터뷰에는 어댑터가 설정되어야 합니다.
    2. 어댑터뷰는 항목을 표시하기 위해서 먼저 표시할 항목의 총 개수를 알 필요가 있을 것입니다. 이 때, 어댑터 뷰는 어댑터의 getCount()란 메소드를 통해 현재 어뎁터가 관리하는 데이터 항목의 총 개수를 반환합니다.
    3. 어댑터 뷰는 어댑터의 getView()란 메소드를 통해서 화면에 실제로 표시할 항목뷰를 얻고, 이를 화면에 표시합니다.
- 사용자가 어댑터뷰의 특정 위치의 항목을 선택하였을 때, 어댑터뷰는 선택된 항목, 항목ID, 항목뷰를 어댑터의 getItem(), getItemId(), getView() 메소드를 통해 얻어와서 이를 항목선택 이벤트 처리기에 넘겨줍니다.
![](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fa997c1d3-9f22-4d76-bd94-f2172ad6e3cd%2FUntitled.png?table=block&id=c2c11087-df58-44b4-949b-ca0e6946bffb&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=1910&userId=&cache=v2)

### 03. 🤔어댑터 종류

- **1) BaseAdapter**
    - **어댑터 클래스의 공통 구현**
    - **사용자 정의 어댑터 구현 시 사용**
    
- **2) ArrayAdapter**
    - **객체 배열이나 리소스에 정의된 배열로부터 데이터를 공급받음**
- **3) CursorAdapter**
    - **데이터베이스로부터 데이터를 공급받음**
- **4) SimpleAdapter**
    - **데이터를 Map(키,값)의 리스트로 관리**
    - **데이터를 XML파일에 정의된 뷰에 대응시키는 어댑터**

![](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fa27d5311-c6e9-4241-a28c-0c162875bc7d%2FUntitled.png?table=block&id=5fd68b03-d035-41a6-9d1c-639e175b5871&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=1670&userId=&cache=v2)

### 2. 리스트 뷰(ListView)

### 01. ❓과연 리스트뷰(ListView)는 무엇일까?

- **ListView는 어댑터 뷰의 대표 위젯으로서, 복수 개의 항목을 수직으로 표시**
``kotlin
 val adapter = ArrayAdapter(this, android.R.layout.simple_list_item_1, items)
```

### 3. 그리드 뷰(GridView)

### 01. ❓과연 그리드 뷰(GridView)는 무엇일까?

- **GridView는 2차원 스크롤 가능한 그리드에 항목을 표시**

### 03. 🤗이미지 그리드 뷰 만들어보기

### 1) 이미지 그리드 뷰 설정 절차

- **Image GridView Test 프로젝트 생성**
- **메인화면 레이아웃에 GridView위젯 정의(XML코드)**
- **어댑터 정의(Kotlin코드)**
- **어댑터를 생성하고 GridView객체에 연결(Kotlin코드)**
 
 Adapter정의
그리드 뷰의 항목으로 간단한 텍스트가 아닌 이미지를 사용하고자 하는 경우에는 그리드뷰의 항목으로 이미지를 공급하는 ImageAdapter를 BaseAdapter로부터 파생하여 정의한다.
```kotlin
class ImageAdapter : BaseAdapter() {
    override fun getCount(): Int {
        return mThumbIds.size
    }

    override fun getItem(position: Int): Any {
        return mThumbIds[position]
    }

    override fun getItemId(position: Int): Long {
        return position.toLong()
    }

    override fun getView(position: Int, convertView: View?, parent: ViewGroup?): View {
        val imageView: ImageView
        if (convertView == null) {
            imageView = ImageView(parent!!.context)
            imageView.layoutParams = AbsListView.LayoutParams(200, 200)
            imageView.scaleType = ImageView.ScaleType.CENTER_CROP
            imageView.setPadding(8, 8, 8, 8)
        } else {
            imageView = convertView as ImageView
        }

        imageView.setImageResource(mThumbIds.get(position))
        return imageView
    }

    private val mThumbIds = arrayOf<Int>(
        R.drawable.sample_2, R.drawable.sample_3,
        R.drawable.sample_4, R.drawable.sample_5,
        R.drawable.sample_6, R.drawable.sample_7,
        R.drawable.sample_0, R.drawable.sample_1,
        R.drawable.sample_2, R.drawable.sample_3,
        R.drawable.sample_4, R.drawable.sample_5,
        R.drawable.sample_6, R.drawable.sample_7,
        R.drawable.sample_0, R.drawable.sample_1,
        R.drawable.sample_2, R.drawable.sample_3,
        R.drawable.sample_4, R.drawable.sample_5,
        R.drawable.sample_6, R.drawable.sample_7
    )
}
```
```kotlin
class MainActivity : AppCompatActivity() {

    private lateinit var binding: ActivityMainBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)

        // ImageAdapter 객체를 생성하고 GridView 객체에 연결
        binding.gridview.adapter = ImageAdapter()


    }
}
```