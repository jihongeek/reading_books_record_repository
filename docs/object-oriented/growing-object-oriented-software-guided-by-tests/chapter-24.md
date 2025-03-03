---
sidebar_position: 25
sidebar_label: 24. 테스트 유연성
---

# 🌈 Chapter 24: 테스트 유연성
- 테스트 불안정성의 공통적인 원인은 다음과 같다.
  - 테스트가 시스템에서 관련이 없는 부분이나 테스트 대상 객체에 무관한 행위와 너무 긴밀하게 결햅돼 있다.
  - 테스트가 대상 코드의 예상 행위를 과도하게 기술해서 필요 이상으로 제약한다.
  - 여러 테스트에서 동일한 제품 코드의 행위를 시험할 때 중복이 생긴다.
- 테스트 불안정성은 시스템 설계와도 관련이 있는데 **어떤 객체가 의존성이 너무 많거나 해당 객체의 의존성이 감춰져 있어** 환경과 분리하기가 어렵다면 해당 객체의 테스트는 객체와 동떨어진 부분이 변경될 때 실패할 것이다.
- 테스트 가독성과 회복력은 뗄 수 없는 관계며, 문제에 집중하고, 명료한 준비 사항을 갖추고 있으며, 중복이 최소화된 테스트는 이름을 짓기가 쉽고 테스트 목적이 분명하게 드러난다.

## 📚 표현이 아닌 정보를 위한 테스트
- 테스트가 시스템의 다른 부분에서 표현되는 값에 영향을 받는 구조가 되면 그러한 부분에 대한 의존성이 생기고, 결국 의존하는 부분이 변경되면 테스트도 꺠질 것이다.
- 아래는 특정 이메일 주소에 해당하는 Customer를 찾는 것이다.

```java
public interface CustomerBase {
  // 고객을 찾을 수 없다면 null을 반환
  Customer findCustomerWithEmailAddress(String emailAddress);
  // ...
}

// 테스트
allowing(CustomerBase).findCustomerWithEmailAddress(theAddress);
wil(returnValue(null)); // 널 반환
```

- 여기서 `null`을 사용하는데 문제점은 `null`이 무엇을 의미하고 언제 적절한지 기억해야 한다는 것이다. 즉, 테스트가 자기 서술적이지 않다. 또 다른 점은 유지 보스에 드는 비용이다. 언젠가 `null` 참조가 발생하는 곳을 `CustomerBase`까지 찾아 내려가야 할 것이다.
- 대신 테스트에 '고객을 찾을 수 없음'의 자체적인 표현을 `null` 리터럴 대신 적절한 이름을 지닌 단 한 가지 제약으로 부여한다면 이러한 힘들고 단조로운 일을 피할 수 있을 것이다.

```java
public static final Maybe<Customer> NO_CUSTOMER_FOUND = Maybe.nothing();
```

- 테스트는 객체 간에 **전달된 정보 측면에서 작성**해야 하며, 해당 정보가 어떻게 표현되는지 측면에서 작성해서는 안 된다.
- `NO_CUSTOMER_FOUND` 같은 중요한 값은 상수로 한 곳에서 정의해야 한다.

## 📚 정확한 단정
- 테스트에서는 테스트 중인 시나리오와 관련이 있는 단정에 집중한다. 테스트 입력 값에 좌우되는 단정 값은 자제하고 다른 테스트에서 검사한 행위를 재단정하는 것도 자제한다.
- 테스트 단정은 대부분 동일성을 단순히 확인하는 것에 해당한다.
- 결과가 더 복잡해질 수 있는 방법
1. 결과는 구조적인 값 타입으로 정의될 수 있다. 이는 우리가 단정하고자 하는 속성을 직접 참조할 수 있기 때문에 이해하기 어렵지 않다.
2. 텍스트 문자열에 관해 단정해야 할 때가 있다. 떄때로 텍스트가 정확히 무엇이어야 할지 알고 싶은데, 특정 메시지를 찾아야 할 때가 그렇다. 이때 단지 핵심 정보가 포함돼 있는지만 알고 싶다면 다음과 같이 작성하면 된다.

```java
assertThat(failureMessage, allOf(containsString("strikePrice=92"), containsString("id=FGD.430")));
```

- 이 모든 문자열이 `failureMessage`의 얻ㄴ가에 나타나는지만 단정한다. 이렇게만 해도 확신할 수 있으며, 중요하다고 여겨진다면 다른 테스트를 작성해 메시지가 올바른 포맷으로 돼 있는지 확인할 수 있다.

## 📚 정확한 예상 구문
- 각 목 객체 테스트에서는 테스트 대상 객체와 그러한 객체의 이웃 간의 상호 작용의 관련 세부 사항을 명시해야 한다. 한 객체에 대한 일련의 단위 테스트는 해당 객체가 시스템의 다른 부분과 통신하는 데 필요한 프로토콜을 기술한다.

### 🎈 정확한 매개변수 매칭
- 메서드에 전달하는 값에 관해서도 정확함을 기하고자 한다.

### 🎈 허용과 예상
- jMock은 모든 예상 구문이 테스트 도중에 충족되지만 허용은 일치하거나 그렇지 않을 수도 있다. 이러한 구분의 요점은 **특정 테스트에서 중요한 부분을 강조하는 데 있다.**
- 예상 구문은 테스트하는 프로토콜에 핵심적인 상호 작용을 서술한다. (이 메시지를 객체에 보내면 해당 객체가 이 다른 메시지를 이 이웃 객체에 보낼 것으로 예상한다.)
- 허용은 테스트하는 상호 작용을 보조한다. 테스트 하고 싶은 행위에 대해 객체가 올바른 상태를 지니게 하기 위해 허용을 스텁으로 사용하기도 한다. 이러한 메시지는 다른 테스트에서 다룰 것이다.
- 이 규칙은 테스트된 객체에서 테스트를 분리하는 데 도움이 된다.

### 🎈 무관한 객체 무시하기
- 시험 중인 기능과 무관한 협력 객체를 무시해 테스트를 단순화할 수 있다.
- 이렇게 하면 **테스트가 단순해지고 문제에 집중할 수 있으므로 중요한 바가 무엇이고 코드의 한 측면에 생긴 변화가 관련이 없는 테스트를 깨뜨리지는 않는지 즉시 알 수 있다.**
- 하지만 **무시된 기능도 어딘가에서 테스트해야 하고 모든 것을 함께 돌아가게 하는 고수준 테스트가 있음을 보장해야 한다.**

### 🎈 호출 순서
- jMock에서는 어떤 순서로든 목 객체를 호출할 수 있다. 즉, 예상 구문은 같은 순서로 선언할 필요가 없다.
- **테스트에서 상호 작용 순서에 관해 말하는 바가 적을수록 구현에는 유연선이 더 늘어난다.** 아울러 테스트를 어떻게 구조화하느냐에도 유연성이 생긴다.
- jMock에는 호출 순서를 제약하는 두 가지 메커니즘이 있는데 하나는 시퀸스로 호출하는 순차 목록을 정의하는 것이고 다른 하나는 상태 기계로 좀 더 정교한 순서 제약을 서술할 수 있다.
- 시퀸스는 상태 기계에 비해 이해하기가 더 간단하지만 제약성 탓에 부적절하게 사용할 경우 테스트가 불안정해질 수 있다. 시퀸스는 어떤 객체가 이웃 객체에 올바른 순서로 통지를 보냈는지 확인하는 가장 유용한 수단이다.

### 🎈 jMock 상태의 위력
- States를 이용해 테스트의 세 가지 참가자 유형, 즉 테스트 대상 객체, 해당 객체의 이웃, 그리고 테스트 자체를 모델링할 수 있다.
- 테스트 대상 객체의 상태에 대해 이해한 바를 표현할 수 있다. 테스트는 해당 객체가 이웃 객체에 전달하는 이벤트를 대기하고 있다가 이벤트를 이용해 상태 전이를 일으키고 객체의 프로토콜을 위반하는 이벤트를 거부한다.
- States는 테스트에서 해당 **객체 관해 찾은 관련 사항을 기술**하지, 객체 내부 구조를 기술하지 안흔다. (객체의 구현에 제약 받지 않는다.)

### 🎈 훨씬 더 자유로운 예상 구문
- jMock에는 임의 예상 구문을 정의해 끼워 넣을 수 있는 지점이 있다. 이를테면, 어떤 접근자 메서드를 받아들이게끔 예상 구문을 작성할 수 있다.

```java
allowing(aPeerObject).method(startsWith("get")).withNoArguments();
```

- 또한, 객체 집합 중 하나에 대한 호출을 받아들이게끔 예상 구문을 작성할 수 있다.

```java
oneOf(anyOf(same(o1), same(o2), same(o3))).method("doSomething");
```

## 📚 실험용 쥐 객체
- 어댑터 코드에 대한 테스트를 작성할 떄 가장 쉬운 접근법은 애플리케이션 도메인 모델의 타입을 사용하는 것이다.
- 하지만, 이렇게 하면 애플리케이션과 어댑터 도메인이 걸합되기 때문에 테스트가 불안정해진다. 이 경우 관심사를 분리하지 않았으므로 애플리케이션 모델을 변경했을 때 테스트를 잘못 깨뜨리는 위험이 초래된다.
- 또 다른 문제는 테스트 가정이 깨질 때 이를 파악하기가 더 어렵다는 것이다. 테스트 중에서 작동이 멈춘 것이 있다는 것과 중요한 기능이 다뤄지지 않았다는 사실을 우리에게 알려주는 것이 아무것도 없다.
