# 3장 함수

### 함수
함수를 만드는 방법에 대하여 설명이 존재하는 장이다.

- 목록 3-1
``` java
public static String testableHtml(
  PageData pageData,
  boolean includeSuiteSetup
) throws Exception {
  WikiPage wikiPage = pageData.getWikiPage();
  StringBuffer buffer = new StringBuffer();
  if (pageData.hasAttribute("Test")) {
    if (includeSuiteSetup){
      WikiPage suiteSetup =
        PageCrawlerImpl.getInheritedPage(
            SuiteResponder.SUITE_SETUP_NAME, wikiPage
        );
      if (suiteSetup != null)  {
        WikiPagePath pagePath =
          suiteSetup.getPageCrawler().getFullPath(suiteSetup);
        String pagePathName = PathParser.render(pagePath);
        buffer.append("!include -setup .")
              .append(pagePathName)
              .append("\n");
      }
}
WikiPage setup =
  PageCrawlerImpl.getInheritedPage("SetUp", wikiPage);
if (setup != null) {
  WikiPagePath setupPath =
    wikiPage.getPageCrawler().getFullPath(setup);
  String setupPathName = PathParser.render(setupPath);
  buffer.append("!include -setup .")
        .append(setupPathName)
        .append("\n");
  }
}
buffer.append(pageData.getContent());
if (pageData.hasAttribute("Test")) {
  WikiPage teardown =
    PageCrawlerImpl.getInheritedPage("TearDown", wikiPage);
  if (teardown != null) {
    WikiPagePath tearDownPath =
      wikiPage.getPageCrawler().getFullPath(teardown);
    String tearDownPathName = PathParser.render(tearDownPath);
    buffer.append("\n")
          .append("!include -teardown .")
          .append(tearDownPathName)
          .append("\n")
}
if (includeSuiteSetup) {
  WikiPage suiteTeardown =
    PageCrawlerImpl.getInheritedPage(
          SuiteResponder.SUITE_TEARDOWN_NAME,
          wikiPage
    );
  if (suiteTeardown != null){
    WikiPagePath pagePath =
      suiteTeardown.getPageCrawler().getFullPath (suiteTeardown);
    String pagePathName = PathParser.render(pagePath);
    buffer.append("!include -teardown .")
          .append(pagePathName)
          .append("\n");
      }
    }
  }
  pageData.setContent(buffer.toString());
  return pageData.getHtml();
}
```

- 목록 3-2
``` java
public static String renderPageWithSetipsAndTeardowns(
  PageData pageData, boolean isSuite
) throws Exception {
  boolean isTestPage = pageData.hasAttribute("Test");
  if (isTestPage) {
    WikiPage testPage = pageData.getWikiPage();
    StringBuffer newPageContent = new StringBuffer();
    includeSetupPages(testPage, newPageContent, isSuite);
    newPageContent.append(pageData.getContent());
    includeTeardownPages(testPage, newPageContent, isSuite);
    pageData.setContent(newPageContent.toString());
  } 
  return pageData.getHtml();
}
```

- 목록 3-3
``` java
public static String renderPageWithSetupsAndTeardowns(
  PageData pageData, boolean isSuite) throws Exception {
  if  (isTestPage(pageData))
    includeSetupAndTeardownPages(pageData, isSuite);
  return pageData.getHtml();
}
```

### 작게 만들어라!
목록 3-1은 3분이라는 시간안에 읽고 이해하라 하면 읽고, 이해하기 정말 어려울 것이다.<br/>
또한 코드에는 WikiPage와 wikiPage같이 혼용되는 코드도 존재한다. 그러기 때문에 목록 3-1은 목록 3-2로 리팩터링 하여 더 간결화를 진행해야 하는 코드다.<br/>
하지만 목록 3-2도 최적화된 코드는 아니다. 최적화를 통한다면 목록 3-1 코드를 목록 3-3까지 줄여낼 수 있어야 한다.<br/><br/>

### 블록과 들여쓰기
if 문/else 문/while 문 등에 들어가는 블록은 한 줄이어야 한다.<br/>
대개 여기서 함수를 호출하는데 그러면 바깥을 감싸는 함수(enclosing function)가 작아질 뿐 아니라 블록 안에서 호출하는 함수 이름을 적절히 짓는다면, 코드를 이해하기도 쉬워진다.<br/><br/>


### 한 가지만 해라!
**함수는 한 가지를 해야 한다. 그 한 가지를 잘 해야 한다. 그 한 가지만을 해야 한다.** <br/><br/>

목록 3-3은 다음의 세 가지를 진행한다.<br/>
1. 페이지가 테스트 페이지인지 판단한다.<br/>
2. 그렇다면 설정 페이지와 해제 페이지를 넣는다.<br/>
3. 페이지를 HTML로 렌더링한다.<br/><br/>

하지만 3 가지를 진행한다 해서 목록 3-3가 세 가지 일을 하는 것은 아니다.<br/>

### 함수 당 추상화 수준은 하나로!
함수가 확실한 '한 가지' 작업만 하려면 함수 내 모든 문장의 추상화 수준이 동일해야 한다.<br/>
목록 3-1은 이 규측을 확실하게 위반하며, 추상화 수준이 아주 낮다.<br/><br/>

### 위에서 아래로 코드 읽기: 내려가기 규칙
코드는 위에서 아래로 이야기 처럼 읽혀야 좋다. 한 함수 다음에는 추상화 수준이 한 단계 낮은 함수가 온다.<br/>
위에서 아래로 프로그램을 읽으면 함수 추상화 수준이 한 번에 한 단계씩 낮아진다.<br/>

즉, 가장 큰 추상화 이후에 보다 작은 추상화가 계속 작아지는 단계가 있어야 한다.<br/><br/>


### Switch 문
Switch은 작게 만들기 어렵다. 하지만 다형성(polymorphsim)을 이용하면 비교적 작게 만들 수 있다.

- 목록 3-4
``` java
public Money calculatePay(Employee e)
throws InvalidEmployeeType {
  switch (e.type) {
    case COMMISSIONED:
      return calculateCommissionedPay(e);
    case HOURLY:
      return calculateHourlyPay(e);
    case SALARIED:
      return calculateSalariedPay(e);
    default :
      throw new InvalidEmployeeType(e.type);
  }
}
```
위 함수는 직원 유형에 따라 다른 값을 계산해 반환하는 함수이다. <br/>

목록 3-4는 크게 5가지 문제가 존재한다.<br/>

1. 함수가 길다.<br/>
2. 한 가지 작업만 수행하지 않는다.<br/>
3. SRP(Single Responsibility Principle)를 위반한다.<br/>
4. OCP(Open Closed Principle)를 위반한다.<br/>
5. 목록 3-4 함수와 구조가 동일한 함수가 무한정 존재한다. <br/><br/>

이 문제를 해결한 코드는 다음과 같다.<br/>

- 목록 3-5
``` java
public abstract class Employee{
  public abstract boolean isPayday();
  public abstract Money calculatePay();
  public abstract void deliverPay(Money pay);
}
------------------
public interface EmployeeFactory {
  public Employee makeEmployee(EmployeeRecord r) throws InvalidEmployeeType;
}
------------------
public class EmployeeFactoryImpl implements EmployeeFactory {
  public Employee makeEmployee(EmployeeRecord r) throws InvalidEmployeeType {
    switch (r.type) {
      case COMMISSIONED:
        return new CommissionedEmployee(r);
      case HOURLY:
        return new HourlyEmployee(r);
      case SALARIED:
        return new SalariedEmployee(r);
      default:
        throw new InvalidEmployeeType(r.type);
    }
  }
}
```
이렇게 정리하면 상속 관계로 숨긴 후에는 절대로 다른 코드에 노출하지 않는 장점이 존재한다. 하지만 이렇게 작성하면 규칙을 위반하는 상황도 생긴다. <br/><br/>


### 서술적인 이름을 사용하라!
ex) testableHtml -> SetupTeardownIncluder.render로 변경하는 것을 서술적 이름으로 변경됐음을 말한다.<br/>
"코드를 읽으면서 짐작했던 기능을 각 루틴이 그대로 수행한다면 깨끗한 코드라 불러도 되겠다." 한 가지만 하는 작은 함수에 좋은 일므을 붙인다면 이런 원칙을 달성함에 있어 이미 절반은 성공했다. 또한 함수가 작고 단순할수록 서술적인 이름을 고르기도 쉬워진다.<br/><br/>

이름을 정하느라 시간을 들여도 괜찮다. 이런저런 이름을 넣어 코드를 읽어보면 더 좋으며, 이클립스나 인텔리제이 같은 최신 IDE에서 이름 바꾸기는 식은 죽 먹기이다.<br/>
IDE를 사용해 이런저런 이름을 시도한 후 최대한 서술적인 이름을 골라도 좋다. 또한 이름을 붙일 때는 일관성이 있어야 한다.<br/>
여기서 일관성이란 모듈 내에서 함수 이름은 같은 문구, 명사, 동사를 사용하는 것을 의미한다.<br/><br/>

### 함수 인수
함수에서 이상적인 인수 개수는 0개(무항)다. 다음은 1개(단항)이며, 그 다음은 2개(이항)이다.<br/>
책에서는 3개(삼항)는 가능하면 피하고, 4개 이상의 다항은 특별한 이유가 있어도 사용하지 않는 것을 얘기한다.<br/><br/>

최선은 입력 인수가 없는 경우이며, 차선은 입력 인수가 1개뿐인 경우이다.<br/>
SetupTeardownIncluder.render(pageData)는 이해하기 아주 쉬운데 이 의미는 pageData객체 내용을 렌더링(render)하겠다는 뜻이다.

- 많이 쓰는 단항 형식<br/>
함수에 인수 1개를 넘긴는 이유로 가장 흔한 경우는 두 가지이다.<br/>
1. 인수에 질문을 던지는 경우이다.<br/>
2. 인수를 뭔가로 변환해 결과를 반환하는 경우이다.<br/><br/>

아주 유용한 단항 함수 형식이 이벤트인데 이벤트 함수는 입력 인수만 존재한다.<br/>
이벤트 함수는 조심해서 사용해야 한다. 이벤트 함수는 이름과 문맥을 주의해서 선택해야 한다.<br/>






