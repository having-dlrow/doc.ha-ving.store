# - Template Callback

#### 템플릿 콜백 패턴

* 템플릿/콜백 패턴은 전략 패턴의 일종으로 전략 패턴의 기본적인 구조에 변화되는 부분을 매번 클래스로 만들지 않고 **익명 내부 클래스**를 이용해 바로 생성하여 이용한다.
* 전략 패턴과 스프링의 의존성 주입(DI) 의 장점을 익명 내부 클래스 사용 전략과 결합해 독특하게 활용되는 패턴이다.

**장점**

* 전략 패턴은 따로 전략 알고리즘을 정해놓은 별도의 전략 클래스가 필요했지만 템플릿 콜백 패턴은 별도의 전략 클래스 없이 전략을 사용하는 메소드에 매개 변수 값으로 전략 로직을 넘겨 실행한다.



```
interface OperationStrategy {
    // (int x, int y) -> int
    int calculate(int x, int y);
}

// Template
class OperationTemplate {
    int calculate(int x, int y, OperationStrategy cal) {
    	System.out.println("연산 시작");
        int result = cal.calculate(x, y);
        System.out.println("연산 종료");
        return result;
    }
}

class OperationContext {

    int calculate(int x, String operation, int y) {
        System.out.println("연산 시작");
        int result = execute(operation).calculate(x, y);
        System.out.println("연산 종료");
        return result;
    }

    // 익명 클래스를 Template 클래스 내에 아예 정의함으로써 클라이언트의 전략 주입 중복 코드를 줄임
    private OperationStrategy execute(final String oper) {

        return new OperationStrategy() {
            public int calculate(int x, int y) {
                int result = 0;
                switch(oper) {
                    case "+" : result = x + y; break;
                    case "-" : result = x - y; break;
                    case "*" : result = x * y; break;
                    case "/" : result = x / y; break;
                }
                return result;
            }
        };
    }
}
```

client

```
public class Client {
    public static void main(String[] args) {
        int x = 100;
        int y = 30;

        OperationContext cxt = new OperationContext();

        int result = cxt.calculate(x, y, (x1, y1) -> x1 + y1);
        System.out.println(result); // 130

        result = cxt.calculate(x, y, (x1, y1) -> x1 - y1);
        System.out.println(result); // 70

        result = cxt.calculate(x, y, (x1, y1) -> x1 * y1);
        System.out.println(result); // 3000

        result = cxt.calculate(x, y, (x1, y1) -> x1 / y1);
        System.out.println(result); // 3
    }
}
```
