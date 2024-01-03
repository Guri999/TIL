Scope functions
=
Kotlin 표준 라이브러리에는 객체 컨텍스트 내에서 코드 블록을 실행하는 것이 유일한 목적인 여러 함수가 포함되어 있다

 제공된 람다 식이 있는 개체에서 이러한 함수를 호출하면 임시 범위가 형성됩니다. 이 범위에서는 이름 없이 개체에 액세스할 수 있습니다.
 
 let, run, with, apply, also
 
## 기능선택
 ![](https://velog.velcdn.com/images/guysang/post/0774caef-9853-4d1f-a10a-b5e33a8dad49/image.png)

- nullable이 아닌 객체에 대해 람다 실행:let

- 로컬 범위의 변수로 표현식 소개:let

- 객체 구성:apply

- 객체 구성 및 결과 계산:run

- 표현식이 필요한 명령문 실행: 비확장run

- 추가 효과:also

- 객체에 대한 그룹화 함수 호출:with

## 구별

각 범위 함수에는 두 가지 주요 차이점이 있다

- 컨텍스트 개체를 참조하는 방식

- 반환 값

### Context object: this or it

```kotlin
fun main() {
    val str = "Hello"
    // this
    str.run {
        println("The string's length: $length")
        //println("The string's length: ${this.length}") // does the same
    }

    // it
    str.let {
        println("The string's length is ${it.length}")
    }
}
```
#### this

run, with및 키워드로 apply컨텍스트 개체를 람다 수신기this 로 참조

#### it

함수나 속성을 호출할 때 처럼 암시적으로 객체를 사용할 수는 없다

개체가 함수 it호출에서 인수로 주로 사용될 때 컨텍스트 개체에 액세스하는 것이 더 좋다

it코드 블록에서 여러 변수를 사용하는 경우에도 더 좋다

### 반환값

범위 함수는 반환하는 결과에 따라 다르다

- apply그리고 also는 context object를 반환

- let, run및 with람다 결과를 반환

## 기능


### let
컨텍스트 개체는 인수( it)로 사용할 수 있습니다.

반환 값은 람다 결과입니다.

let호출 체인 결과에 대해 하나 이상의 함수를 호출하는 데 사용할 수 있습니다

### with

컨텍스트 객체는 수신자( this)로 사용 가능합니다.

반환 값은 람다 결과입니다.

확장 함수가 아니기 때문에 with컨텍스트 개체는 인수로 전달되지만 람다 내부에서는 수신자( this)로 사용할 수 있습니다.

### run

컨텍스트 객체는 수신자( this)로 사용 가능합니다.

반환 값은 람다 결과입니다.

run와 동일 with하지만 확장 기능으로 구현됩니다. 처럼 let점 표기법을 사용하여 컨텍스트 객체에서 호출할 수 있습니다.

### apply

컨텍스트 객체는 수신자( this)로 사용 가능합니다.

반환 값은 객체 자체입니다.

컨텍스트 개체 자체를 반환 하므로 apply값을 반환하지 않고 주로 수신자 개체의 멤버에 대해 작동하는 코드 블록에 사용하는 것이 좋습니다.

### also

컨텍스트 개체는 인수( it)로 사용할 수 있습니다.

반환 값은 객체 자체입니다.

also컨텍스트 개체를 인수로 사용하는 일부 작업을 수행하는 데 유용합니다. 해당 속성 및 함수 대신 개체에 대한 참조가 필요한 작업에 사용하거나 외부 범위에서 참조를 also숨기고 싶지 않을 때 사용합니다.