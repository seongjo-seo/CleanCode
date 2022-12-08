# 05장 형식맞추기

### 형식을 맞추는 목적
코드 형식은 매우 중요하다.<br/>
오랜 시간이 지난 후 원래 코드의 흔적을 더 이상 찾아보기 어려울 정도로 코드의 형태가 완전히 바뀌더라도 맨 처음 잡아 놓은 형식 규칙이 유지보수 단계까지도 구현 스타일과 가독성 그리고 확장성까지 영향을 미친다.<br/>
원활한 소통을 장려하기 위한 형식을 다루는 챕터이다.<br/>


- 적절한 행 길이를 유지하라.<br/>
행 수를 큰 파일보다 작은 파일로 최대한 협업에 있어서 이해하기 쉽게 크기를 규정하라.<br/>


- 신문 기사처럼 작성하라.<br/>
첫 문단은 전체 기사 내용을 요약하듯 작성하며, 세세한 사실은 숨기고 커다란 그림들을 보여주는 과정을 진행한다.<br/>
위에서 아래로 읽으며 내려가면 세세한 사실이 조금씩 드러날 수 있도록 작성하는 것이다.<br/>
신문에서 작성되는 제목, 날짜, 이름, 발언, 주장, 기타 세부 사항 등과 같이 코드도 상세하게 기승전결을 추구하자.<br/>


- 개념은 빈 행으로 분리하라.<br/>
거의 모든 코드는 대부분 왼쪽에서 오른쪽으로 위에서 아래로 코드를 읽어내린다.<br/>
개념의 시작과 끝은 마무리하는 것을 권장하자.<br/>
예를 들면 패키지 선언부, import 문, 각 함수 사이에 빈 행을 추가하여 의미를 정확하게 맞춰준다.<br/>


- 세로 밀집도<br/>
줄 바꿈이 개념을 분리한다면 세로 밀집도는 연관성을 의미한다.<br/>
서로 밀접한 코드 행은 세로로 가까이 놓여야 의미가 있다.<br/>


- 수직 거리<br/>
흩어 놓은 조각은 시선을 분리하고, 원하는 조각을 찾아내기 어렵게 만든다.<br/><br/>

서로 밀접한 개념은 세로로 가까이 둬야 한다.<br/>
두 개념이 하나의 파일 내부에 속하지 않는다면 규칙은 있으나 마나 한 것이 된다.<br/>
같은 파일에 속할 정도로 밀접한 두 개념인 경우. 세로 거리로 연관성을 표현하는 것을 권장한다<br/>


- 변수 선언<br/>
변수는 사용하는 위치에 최대한 가까이 선언하는 것을 권장한다.<br/>
인스턴스 변수의 경우. 변수 간에 세로로 거리를 두지 않는다. 잘 설계한 클래스는 많은 클래스 메서드가 인스턴스 변수를 사용하기 때문이다<br/>

C++의 경우는 모든 인스턴스 변수를 클래스 마지막에 선언하는 가위 룰(scissors rule)을 적용한다. 하지만 Java의 경우는 보통 클래스 맨 처음에 인스턴스 변수를 선언한다.<br/>

- 종속 함수<br/>
A 함수는 호출하는 B 함수는 호출되는 종속된 함수의 형태라면 두 함수는 세로로 가까이 배치한다.
그리고 가능하면 호출하는 A 함수를 호출되는 B 함수를 순서대로 배치한다. 이렇게 배치하는 것이 자연스럽게 읽힐 수 있으며, 가독성이 좋아진다.<br/><br/>

- 개념적 유사성<br/>
개념적 유사성은 예로 들면 함수가 기본 명명법이 똑같고 기본 기능이 유사하고 간단한 경우이다.<br/>
또한 서로가 서로를 호출하는 관계에서는 부차적인 요인이 된다.

- 세로 순서<br/>
종속성은 일반적으로 아래 방향으로 유지하게 된다.<br/>

- 가로 형식 맞추기<br/>
가로 형식을 맞추면 읽기가 매우 편해진다. 스크롤을 내려야 할 수 있으나 한 줄 한 줄 읽어내는 것이 쉬워지는 장점이 존재하므로 가능하면 글자를 제한하는 것을 지향한다.<br/>
예전에 홀러리스(Hollerith)가 내놓은 80자 제한도 좋다 하지만 다소 인위적일 수 있다. 100자나 120자에 달하는 규격도 좋은 방향이다.<br/>


- 가로 공백과 밀집도<br/>
가로로는 공백을 사용해 밀접한 개념과 느슨한 개념을 표현하는 것을 목표한다.<br/>
공백으로 개념을 정리 분리하는 것도 가능하다. 하지만 공백을 넣어줘도 IDE나 도구에서 공백을 자동으로 없애는 경우가 흔하기 때문에 초반 설정에서 의논하여 작성하는 것이 좋다.<br/>


- 가로 정렬<br/>
만약 정렬이 필요할 정도로 코드 목록이 길다면 목록의 길이가 문제이지 정렬이 부족한 것은 아닐 것이다. 정렬이 필요하면 선언 부가 길다면 클래스를 쪼개서 작성해야 한다는 의미이다.<br/>


- 들여쓰기<br/>
범위(scope)로 이뤄진 계층을 표현하기 위해 코드를 들여쓴다.<br/>
프로그래밍에서는 왼쪽으로 들여쓰기를 맞춰 코드가 속하는 범위를 시각적으로 표현한다.<br/>
들여쓰기를 올바르게 했을 때. 변수, 생성자 함수, 접근자 함수, 메서드가 금방 보이게 된다.<br/>


- 팀 규칙<br/>
팀 규칙을 통해서 소프트웨어가 일관적인 스타일을 보일 수 있도록 지향한다.<br/>
좋은 소프트웨어 시스템은 읽기 쉬운 문서로 이뤄진다는 사실을 기억해야 한다.<br/>
한 소스 파일에서 봤던 형식이 다른 소스 파일에도 재사용 가능할 수 있을 정도로 신뢰가 가능해야 하며, 온갖 스타일을 뒤섞어 소스 코드를 필요 이상으로 복잡하게 만드는 실수를 지양해야 한다.<br/>


- 밥 아저씨의 형식 규칙<br/>
다음과 같은 코드가 최고의 구현 표준 문서가 되는 예시이다.<br/>
```java
public class CodeAnlyzer implements JavaFileAnalysis{
  private int lineCount;
  private int maxLineWidth;
  private int widestLineNumber;
  private LineWidthHistogram LineWidthHistogram;
  private int totalChars;
  
  public CodeAnalyzer(){
    lineWidthHistogram = new LinewWidthHistogram();
  }
  
  public static List<File> findJavaFiles(File parentDirectory) {
    List<File> files = new ArrayList<File>();
    findJavaFiles(parentDirectory, files);
    return files;
  }
  
  private static void findJavaFiles(File parentDirectory, List<File> files) {
    for (File file : parentDirectory.listFiles()){
      if (file.getName().endsWith(".java"))
        files.add(file);
      else if (file.isDirectory())
        findJavaFiles(file, files);
      }
  }
  
  public void analyzeFile(File javaFile) throws Exception {
    BufferedReader br = new BufferedReader(new FileReader(javaFile));
    String line;
    while ((line = br.readLine()) != null)
      measureLine(line);
  }
  
  private void measureLine(String line){
    lineCount++;
    int lineSize = line.length();
    totalChars += lineSize;
    lineWidthHistogram.addLine(lineSize, lineCount);
    recordWidestLine(lineSize);
  }
  
  private void recordWidesLine(int lineSize) {
    if (lineSize > maxLineWidth){
      maxLineWidth = lineSize;
      widestLineNumber = lineCount;
    }
  }
  
  public int getLineCount(){
    return lineCount;
  }
  
  public int getMaxLineWidth() {
    return maxLineWidth;
  }
  
  public int getWidestLineNumber() {
    return widestLineNumber;
  }
  
  public LineWidthHistogram getLineWidthHistogram() {
    return lineWidthHistogram;
  }
    
```
