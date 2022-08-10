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



