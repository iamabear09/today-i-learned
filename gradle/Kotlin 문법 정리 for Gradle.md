
### 고차함수 / 람다함수

```
fun main(){
    b(::a)

    /* 
     * 람다 함수로 작성된 c
     * (입력 타입) -> 반환 타입 = {변수이름: 입력타입 -> 구문}
     * var c: (String) -> Unit = { s : String -> println(s)}  // 함수 본문에서 파리미터 타입 생략 가능
     * var c: (String) -> Unit = { s -> println(s)}
     */
    var c: (String) -> Unit = { s -> println(s)}

    /*
     * 함수 타입 생략 가능
     * var d: (String) -> Unit = {s: String -> println(s)}
     * var d = {s: String -> println(s)}
     * 타입추론 기능을 이용한 변수의 타입 생략
     */
    var d = {s: String -> println(s)}

    /* 
     * 인자가 없는 경우 변수를 받아오는 부분도 생략 가능
     */
    var e:() -> Unit = {println("파라미터가 없는 람다 식")}
    var f = {
        println("xzcxc")
    }

    /* 
     * 인자가 하나일 경우 it 키워드 사용
     */
    var g : (String)->Unit = {println(it)}

}

fun a(str: String): String {
    println("$str 함수 a")
}

fun b (function: (String) -> Unit) {
    funtion("b가 호출한")
}
```

함수의 마지막 파라미터가 람다식인 경우
```
fun downloadData(url: String, completion: ()-> Unit) {
   completion()
}
/* completion: ()-> Unit 까지의 람다식이 하나의 파라미터이다.
  ()->Unit의 의미는 파라미터가 없고, Unit 즉 아무것도 반환되지 않는 function */

downloadData("myUrl.com", {
   println("completion이 완료돼야 이 글이 출력됩니다.")
   /* downloadData function의 두 파라미터인 String과 람다식 파라미터를 입력함. */
})

```


마지막 파라미터가 람다식 이면, 중괄호 `{ }` 부분을 소괄호 밖으로 뺄 수 있다.
그 파라미터가 한 개면, 생략 후 ‘it’을 사용하여 대체 가능하다.
```
fun downloadWeather (url: String, completion: (String) -> Unit) {
   val weatherData = "Cloudy, -3℃"
   /* url에서 데이터를 가져온 후, 아래의 String 변수 weatherData에 저장 */
   completion(weatherData)
}


downloadWeather("weatherUrl.com") { weatherData ->
   println(weatherData)
}

downloadWeather("weatherUrl.com") {
   println(it)
}

```


### 스코프 함수

함수형 언어를 좀 더 편리하게 사용할 수 있도록 하는 기본 함수
`apply, run, with, also, let` 존재한다.

**apply**
인스턴스의 값을 람다함수를 사용해 변경할 수 있는 함수 그리고 변경된 객체를 반환
참조 연산자 없이 인스턴스의 속성을 사용할 수 있다.
```
fun main() {
    var a = Book("a", 20000)
    //apply 스코프람다함수를 통해 a객체의 속성과 함수 변경및 사용가능
    a.apply {		
        name = "apply $name"
        //2000 감소
        dc()
    }
    a.printName()
}

class Book(var name: String, var price: Int) {
    fun dc() {
        price -= 2000
    }

    fun printName() {
        println("$name $price")
    }

```

**출력**
```
apply a 18000
```

**let**
it 참조를 통해 인스턴스에 접근한다.
```
fun main() {
    var price = 5000
    var a = Book("a", 20000)
    a.let{
        println(it.price)
    }
}

class Book(var name: String, var price: Int) {

}
```