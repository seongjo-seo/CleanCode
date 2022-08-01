# 의미 있는 이름 (Tim Ottinger)

### 의도를 분명히 밝혀라
다른 사람이 봐도 직관적인 이름으로 작명하라. <br/>

``` java
int elapsedTimeInDays;
int daysSinceCreation;
int daysSinceModification;
int fileAgeInDays;
```
<br/>

``` java
public List<int []> getThem() {
  List<int[]> list1 = new ArrayList<int[]>();
  for (int[] x ; theList)
    if (x[0] == 4)
      List1.add(x);
    return list1;
}
```
<br/>
변수의 존재 이유, 수행 기능, 사용 방법 등을 주석으로 작성하지 않아도 이해가 쉽게 되는 **이름**이 의도를 잘 갖고 있는 잘 만든 변수이다. <br/>
잘 만든 변수는 주석이 없어도 이해할 수 있다. <br/>

``` java
public List<int []> getFlaggedCells() {
  List<int[]> flaggedCells = new ArrayList<int[]>();
  for (int[] cell : gameBoard)
    if (cell[STATUS_VALUE] == FLAGGED)
      flaggedCells.add(cell);
     return flaggedCells;
}
```
의도가 잘 드러나는 이름을 사용해야 코드 이해와 변경이 쉬워진다. <br/>

``` java
public List<Cell> getFlaggedCells() {
  List<Cell> flaggedCells = new ArrayList<Cell>();
  for (Cell cell : gameBoard)
    if (cell.isFlagged())
      flaggedCells.add(cell);
    return flaggedCells;
}
```

<br/><br/>


### 그릇된 정보를 피해라
일관성이 떨어지는 표기법은 **그릇된 정보**이다.<br/>
대문자 L이 소문자 l이 될 때 1과 비슷한 코드가 되는 이유, 대문자 O의 경우 숫자 0와 유사하게 보이는 것은 코드를 읽는 사람을 헷갈리게 한다.<br/>

```java
int a = l;
if ( O == 1 )
a = Ol;
else
l = 01;
```
<br/><br/><br/>


### 의미 있게 구분하라
컴파일러 또는 인터프리터를 통과하는 것만을 초점으로 잡고 구현한 코드는 문제를 일으킬 수 있다.

``` java
public static void copyChars(char a1[], char a2[]){
  for (int i=0; i< a1.length; i++){
    a2[i] = a1[i];
  }
}
```
위와 같이 컴파일러를 통과하기 위한 언어는 구현한 저자의 의도가 드러나지 않게 된다.<br/>
오류의 예는 다음과 같다.
``` java
getActiveAccount();
getActiveAccounts();
getActiveAcoountInfo();
```
비슷한 단어로 변수를 작성하지 말고 읽는 사람이 명확하게 차이를 느낄 수 있을만한 이름으로 지어야 한다.
<br/><br/>


### 발음하기 쉬운 이름을 사용하라
사람은 단어에 능숙하고, 우리 두뇌에서는 상당 부분을 단어라는 개념만 전적으로 처리한다.<br/>
``` java
class DtaRcrd102{
  private Date genymdhms;
  private Date modydhms;
  private final String pszqint = "102";
  /* ... */
};
```
와
``` java
class Customer {
  private Date generationTimestamp;
  private Date modificationTimestamp;
  private final String recordId = "102";
  /* ... */
};
```
pszqint 봐주세요와 recordId 봐주세요는 부르는 발음의 차이도 존재하고, 후자는 더 읽기 쉽고 직관적이다.
<br/><br/><br/>

### 검색하기 쉬운 이름을 사용하라
메서드에서 로컬 변수만 한 문자를 사용한다.<br/>
이름 길이는 범위 크기에 비례해야 한다.<br/>
변수나 상수를 코드 여러 곳에서 사용한다면 검색하기 쉬운 이름이 바람직하다.
<br/><br/><br/>

### 인코딩을 피하라
유형이나 범위 정보까지 인코딩에 넣으면 그만큼 이름을 해독하기 어려워진다.<br/>
헝가리식 표기법 <br/>
과거 윈도 C API는 헝가리식 표기법을 굉장히 중요하게 여겼다.<br/>
이때 윈도 C API는 모드 변수가 정수 핸들, long 포인터, void 포인터, (속성과 용도가 다른) 여러 문자열 중 하나였다.<br/><br/>
최근에 나오는 프로그래밍 언어는 훨씬 많은 타입을 지원하면서 컴파일러가 변수 타입을 기억하고 강제한다.
그리고 클래스와 함수는 점차 작아지는 추세이다. <br/>
이제는 헝가리식 표기법이나 기타 인코딩 방식이 오히려 코딩에 방해가 될 뿐이다. <br/>
변수, 함수, 클래스 이름이나 타임을 바꾸기가 어려워지며, 읽어도 어려워지기 때문에 잘못 읽을 경우가 커진다.<br/>

``` java
PhoneNumber phoneString;
// 타입이 바뀌어도 이름은 바뀌지 않는다!
```
### 멤버 변수 접두어
이제는 멤버 변수에 m_ 이라는 접두어를 붙일 필요가 없다. 멤버 변수를 다른 색상으로 표시하여 보기 편하게 하는 IDE를 사용하는 것이 훨씬 좋은 방법이 됐다. <br/>

### 인터페이스 클래스와 구현 클래스
물론 인코딩이 아예 필요가 없는 것은 아니다.<br/>
인터페이스 클래스와 구현 구체 클래스를 구분할 때 사용된다. Ex) 이름Imp
<br/><br/><br/>

### 자신의 기억력을 자랑하지 마라
전문가 프로그래머는 명료함이 최고라는 사실을 이해한다.<br/>
전문가 프로그래머는 자신의 능력을 좋은 방법으로 사용해 남들이 이해하기 쉬운 코드를 내놓는다.<br/>
<br/><br/>
### 클래스 이름
클래스 이름과 객체 이름은 **명사**나 **명사구**가 적합하다.<br/>
좋은 예 : Customer, WikiPage, Account, AddressParser 등<br/>
나쁜 예 : Manager, Processor, Data, Info 등과 같은 단어는 피할 것<br/>
동사는 사용하지 않는다. <br/><br/>
<br/>
### 메서드 이름
메서드 이름은 **동사**나 **동사구**가 적합하다.<br/>
좋은 예 : postPayment, deletePage, save 등이 좋다.<br/>
접근자(Accessor), 변경자(Mutator), 조건자(Predicate)는 javabean 표준에 따라 값 앞에 get, set, is를 붙인다.

``` java
string name = employee.getName();
customer.setName("mike");
if (paycheck.isPosted())...
```
생성자(Constructor)를 중복 정의(overload)할 때는 정적 팩토리 메서드를 사용한다.<br/>

아래의 메서드 인수를 설명하는 것을 예로 한다.

``` java
Complex fulcrumPoint = Complex.FromRealNumber(23.0);
```
위의 코드가 아래 코드보다 좋다.
``` java
Complex fulcrumPoint = new Complex(23.0);
```
<br/><br/><br/>


### 기발한 이름은 피하라
너무 기발하면 저자와 유머 감각이 비슷한 사람만, 그리고 농담을 기억하는 동안만, 이름을 기억한다. 그렇기 때문에 재미난 이름보다 명료한 이름을 선택하라.<br/>
의도를 분명하고 솔직하게 표현하라.<br/><br/><br/>

### 한 개념에 한 단어를 사용하라
추상적인 개념 하나에 단어 하나를 선택해 이를 고수하라.<br/>
메서드 클래스마다 fetch, retrieve, get으로 제각각 부르면 헷갈리게 된다.<br/>
메서드 이름은 독자적이고 일관적이어야 한다. 그래야 프로그래머가 올바른 메서드를 선택할 수 있게 된다.<br/>
이 책은 일관성 있는 어휘를 지향한다.
<br/><br/><br/>

### 말장난을 하지 마라
한 단어를 두 가지 목적으로 사용하지 마라.<br/>
프로그래머는 코드를 최대한 이해하기 쉽게 짜야 한다. <br/>
대충 훑어봐도 이해할 수 있는 코드를 만드는 것이 목표가 돼야 한다.<br/><br/><br/>

### 해법 영역에서 가져온 이름을 사용하라
코드를 읽을 사람도 프로그래머라는 사실을 명심할 것.<br/>
전산 용어, 알고리즘 이름, 패턴 이름, 수학 용어 등을 사용하는데 두려움을 갖지 말 것<br/>
기술 개념에는 기술 이름이 가장 적합한 선택이다.<br/><br/><br/>

### 문제 영역에서 가져온 이름을 사용하라
적절한 '프로그래밍 용어'가 없다면 문제 영역에서 이름을 가져온다. 이렇게 되면 코드를 보수하는 유지 보수 분야 전문가 프로그래머에게 의미를 물어 파악할 수 있다.<br/>
우수한 프로그래머와 설계자라면 해법 영역과 문제 영역을 구분할 줄 알아야 한다.<br/>
문제 영역 개념과 관련이 깊은 코드라면 문제 영역에서 이름을 가져와야 한다.<br/><br/><br/>

### 의미 있는 맥락을 추가하라
스스로 의미가 분명한 이름이 없지 않다.<br/>
클래스, 함수, 이름 공간에 넣어 맥락을 부여하는데 이때 모든 방법이 실패하면 마지막 수단으로 접두어를 붙인다.
ex) firstName, lastName, street, houseNumber, city, state, zipcode라는 변수들이 있다.

함수 이름은 맥락 일부만 제공하며, 알고리즘이 나머지 맥락을 제공하는 예시이다.
이 예시는 함수를 끝까지 읽어보고 나서야 변수 세 개가 '통계 추측(guess statistics)' 메시지에 사용된다는 것을 알 수 있다.
``` java
// 맥락이 불분명한 변수
private void printGuessStatistics(char candidate, int count) {
  String number;
  String verb;
  String pluralModifier;
  if (count == 0){
    number = "no" ;
    verb - "are";
    pluralModifier = "s";
  } else if (count == 1) {
    number = "1";
    verb = "is";
    pluraModifier = "";
  } else {
    number = Integer.toString(count);
    verb = "are";
    pluralModifier = "s";
  }
  String guessMessage = String.format(
    "There %s %s %s%s", verb, number, candidate, pluralModifier
  );
  print(guessMessage);
} 
```

반대로 맥락이 분명하고 확실하게 보이는 알고리즘을 예시로 든다.
``` java
public class GuessStatisticsMessage {
private String number;
private String verb;
private String pluralModifier;

public String make(char candidate, int count){
  createPluralDependentMessageParts(count);
  return String.format(
    "There %s %s %s%s",
      verb, number, candidate, pluralModifier );
}

private void createPluralDependentMessageParts(int count) {
  if (count == 0){
    thereAreNoLetters();
  } else if ( count == 1 ) {
    thereIsOneLetter();
  } else {
    thereAreManyLetters(count);
  }
}

private void thereAreManyLetters(int count) {
  number = Integer.toString(count);
  verb = "are";
  pluralModifier = "s";
}

private void thereIsOneLetter() {
  number = "1";
  verb = "is";
  pluralModifier = "";
}

private void thereAreNoLetters() {
  number = "no";
  verb = "are";
  pluralModifier = "s";
}
}
```
<br/><br/>

### 불필요한 맥락을 없애라
IDE에서 첫 글자를 기준으로 자동 완성 키가 실행되면서 모든 클래스를 열거하기 때문에 클래스 이름에 맞춰서 모든 클래스를 맞춰서 만드는 것은 비효율적이다.<br/>
일반적으로는 짧은 이름이 긴 이름보다 좋다. 하지만 이런 부분은 의미가 분명한 경우에 한에서만 가능한 부분이다.<br/>
이름에 불필요한 맥락을 추가하지 않도록 주의한다.<br/>
