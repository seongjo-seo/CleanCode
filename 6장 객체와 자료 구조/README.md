# 06장 객체와 자료 구조
변수를 private으로 정의하는 이유는 남들이 변수에 의존하지 않게 만들고 싶어서다.<br/>
잘못된 코드 구현은 private을 public과 동일하게 사용하는 것과 같다.<br/>

- 자료 추상화

구체적인 Point 클래스
``` java
public class Point {
  public double x;
  public double y;
}
```
추상적인 Point 클래스
``` java
public interface Point {
  double getX();
  double getY();
  void setCartesian(double x, double y);
  double getR();
  double getTheta();
  void setPolar(double r, doulbe theta);
}
```

구체적인 클래스의 경우 직교좌표계를 사용하고 있으며, 개별적으로 좌표값을 읽고 설정하게 강제한다. 하지만 private으로 변수를 설정하여 getter/setter를 사용하더라도 외부로 값을 노출하여 구현한 것과 다름이 없다.<br/>



- 자료/객체 비대칭


- 디미터 법칙


- 기차 충돌


- 잡종 구조


- 구조체 감추기


- 자료 전달 객체



- 활성화 레코드<br/>
