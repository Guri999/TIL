# RecyclerView
중요 완벽하게 이해해야함

모든 코드를 `이해`해야함

코드는 어디에든 저장해놨다가 사용하는 것

### 1**. RecyclerView**

### 01. 과연 **RecyclerView**는 무엇일까?

RecyclerView는 안드로이드 앱에서 리스트 형태의 데이터를 표시하는데 사용되는 위젯입니다. 여러 아이템을 스크롤 가능한 리스트로 표현하며, 많은 아이템을 효율적으로 관리하고 보여주는 역할을 합니다.

- **RecyclerView는 한정적인 화면에 많은 데이터를 넣을 수 있는 View입니다.**
- **Recycle을 한국어로 하면 재활용하다라는 뜻입니다.**
- **즉, View를 재활용해서 사용하겠다는 말입니다.**
![](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F3c3f6eb3-dceb-4d98-a2cb-b7f3b773687b%2FUntitled.png?table=block&id=31267adf-a0c1-401d-a905-b0e472c2649d&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=580&userId=&cache=v2)

### 02. 🤗 ListView 와 RecyclerView

### **ListView**

- 사용자가 스크롤 할 때마다 위에 있던 아이템은 삭제되고, 맨 아래의 아이템은 생성 되길 반복합니다
- 아이템이 100개면 100이 삭제 생성됩니다. 즉 계속 삭제와 생성을 반복하므로 성능에 좋지않습니다.
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6c8346ba-da65-45d2-8e2a-a63a64d03943/Untitled.png)
    

### RecyclerView

- 사용자가 스크롤 할 때, 위에 있던 아이템은 재활용 돼서 아래로 이동하여 재사용 합니다.
- 즉 아이템이 100개여도 10개정도의 View만 만들고 10개를 재활용해서 사용합니다.
- View를 계속 만드는 ListView의 단점을 보완하기 위해 나왔습니다.
- 계속 만드는 ListView의 단점을 보완하기 위해 나왔습니다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/751994b4-966e-40b3-bd7a-02c64e596dc1/Untitled.png)


리스트 뷰는 싹다 만들고, 리사이클러 뷰는 쓰던칸에 내용물을 바꿔서 사용 < 매우 효율적

### 3. 🤗 RecyclerView사용하기

### 1) Adapter

- Adapter란 데이터 테이블을 목록 형태로 보여주기 위해 사용되는 것으로, 데이터를 다양한 형식의 리스트 형식을 보여주기 위해서 데이터와 RecyclerView 사이에 존재하는 객체이다.
- 즉 데이터와 RecyclerView 사이의 통신을 위한 연결체이다.
예) 전기를 쓰기위한 Input은 똑같은대 220V 110V든 어댑터에 따라 바뀜, 그런 연결해주는 주체 어떤 내용물이든 어댑터에 들어가면 어댑터에 따라 화면에 표시되는 모습이 달라짐

### 2) ViewHolder

- ViewHolder란 화면에 표시될 데이터나 아이템들을 저장하는 역할 입니다.
- RecyclerView의 개념을 적용하기위해선 스크롤 해서 위로 올라간 View를 재활용하기 위해서 이 View를 기억하고 있어야 합니다. ViewHolder가 그역할을 합니다.

리사이클러뷰는 삭제되는 게아니라 재활용하는거기땜에 기억해야함

```kotlin
class MainActivity : AppCompatActivity() {

    private lateinit var binding: ActivityMainBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)

        // 데이터 원본 준비
        val dataList = mutableListOf<MyItem>()
        dataList.add(MyItem(R.drawable.sample_0, "Bella", "1"))
        dataList.add(MyItem(R.drawable.sample_1, "Charlie", "2"))
        dataList.add(MyItem(R.drawable.sample_2, "Daisy", "1.5"))
        dataList.add(MyItem(R.drawable.sample_3, "Duke", "1"))
        dataList.add(MyItem(R.drawable.sample_4, "Max", "2"))
        dataList.add(MyItem(R.drawable.sample_5, "Happy", "4"))
        dataList.add(MyItem(R.drawable.sample_6, "Luna", "3"))
        dataList.add(MyItem(R.drawable.sample_7, "Bob", "2"))

        val adapter = MyAdapter(dataList)
        binding.recyclerview.adapter = adapter
        binding.recyclerview.layoutManager = LinearLayoutManager(this)

        adapter.itemClick = object :MyAdapter.ItemClick {
            override fun onClick(view: View, position: Int) {
                val name: String = dataList[position].aName
                Toast.makeText(this@MainActivity, " $name 선택", Toast.LENGTH_SHORT).show()
            }
        }
    }
}
```
```kotlin
package com.example.myapplication

import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import androidx.recyclerview.widget.RecyclerView
import com.example.myapplication.databinding.ItemRecyclerviewBinding

/*
* 어댑터를 생성할때 메인 액티비티에서 샘플데이터를 mItem에
* */
class MyAdapter(val mItems: MutableList<MyItem>) : RecyclerView.Adapter<MyAdapter.Holder>() {

    /*
    인터페이스로 아이템 클릭을 만들고 메인 액티비티에서 호출
     */
    interface ItemClick {
        fun onClick(view : View, position : Int)
    }

    var itemClick : ItemClick? = null

    /*
    뷰홀더가 뭐냐? -> 재사용하기위한 아이템을 저장하는 역활 홀더
    처음에 onCreate부터 홀더를 만들어줘야 되야하는대 인플레이트해서 레이아웃 인플레이터를쓰고
    binding을 만들어주고 홀더에 넣어줌
     */
    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): Holder {
        val binding = ItemRecyclerviewBinding.inflate(LayoutInflater.from(parent.context), parent, false)
        return Holder(binding)
    }

    /*
    하나하나씩 실행
    여기서 홀더들이 주르르륵 나타내기 시작
    보이는대까지만 실행한다
    2가지방법으로 클릭이벤트를 줄수 있는데
    이 예제는 어댑터에서 클릭이벤트를 받고 이 이벤트를 메인 액티비티로 넘겨줌
    -> 실제로도 많이 쓰는 방법인데 이러면 어댑터랑 메인 액티비티를 이어줄 인터페이스가 필요함
     */
    override fun onBindViewHolder(holder: Holder, position: Int) {
        holder.itemView.setOnClickListener {  //클릭이벤트추가부분
            itemClick?.onClick(it, position) //해당클릭이 일어난 포지션을 매개로 넘김
        }
        holder.iconImageView.setImageResource(mItems[position].aIcon)
        holder.name.text = mItems[position].aName
        holder.age.text = mItems[position].aAge
    }

    override fun getItemId(position: Int): Long {
        return position.toLong()
    }

    //꼭 오버라이드 해줘야함
    override fun getItemCount(): Int {
        return mItems.size
    }

    /*
    * ItemRecyclerviewBinding 이거 어디임? -> xml item_recyclerview의 뷰홀더
    * */
    inner class Holder(val binding: ItemRecyclerviewBinding) : RecyclerView.ViewHolder(binding.root) {
        val iconImageView = binding.iconItem
        val name = binding.textItem1
        val age = binding.textItem2
    }
}
```