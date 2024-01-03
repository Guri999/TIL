ActivityResultContract에서 관계 맺게 해줌
콜백은 거기서 객체 뺴옴

```kotlin
val getContent = registerForActivityResult(GetContent()) { uri: Uri? ->
    // Handle the returned Uri
}
```

registerForActivityResult()는 콜백을 등록하지만, 다른 활동을 실행하거나 결과 요청을 시작하지 않습니다.

이 작업은 반환된 ActivityResultLauncher 인스턴스가 담당

입력이 있으면 런처는 ActivityResultContract 유형과 일치하는 입력을 가져옵니다. launch()를 호출하면 결과를 생성하는 프로세스가 시작

ActivityResultCallback의 onActivityResult()가 다음 예와 같이 실행됩니다
```kotlin
val getContent = registerForActivityResult(GetContent()) { uri: Uri? ->
    // Handle the returned Uri
}

override fun onCreate(savedInstanceState: Bundle?) {
    // ...

    val selectButton = findViewById<Button>(R.id.select_button)

    selectButton.setOnClickListener {
        // Pass in the mime type you want to let the user select
        // as the input
        getContent.launch("image/*")
    }
}
```

lateinit

val a = registerForActivityResult(altEnter.StartActivityForResult) { result ->
if(result.resultCode == Activity.RESULT_OK)
// 로직 수행
}