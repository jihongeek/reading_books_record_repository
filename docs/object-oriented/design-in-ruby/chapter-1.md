---
sidebar_position: 2
---

# ✌️ Chapter 1: 객체지향 디자인

- 객체지향 디자인은 세상을 이미 정해진 절차들의 묶음으로 생각하지 않고, 객체가 서로 주고 받는 메시지들의 연쇄로 파악할 것을 요구한다.

### 📚 디자인 예찬

#### 🎈 디자인이 해결해 줄 수 있는 문제들
- 변화는 어디에나 있고 모든 곳에 있으며 피할 수 없다.
- 변화가 필요하기 때문에 디자인이 중요한 것이다.
- 변화를 주기 힘든 애플리케이션은 수정을 하려면 많은 시간이 필요하고, 다음번 수정이 더욱 어려워진다.

#### 🎈 왜 수정은 어려운가
- 깩체지향 애플리케이션은 상호작용하는 여러 부분으로 구성되어 있고, 각 부분 사이의 상호작용이 전체의 작동을 만들어 낸다.
- 이 여러 부분이 **객체**이고, 객체 사이의 상호작용은 객체가 주고 받는 **메시지** 속에 녹아 있다.
- 수신하는 객체에 대한 이 지식이 두 객체 사이의 의존성을 만들어 내고, 이런 의존성이 애플리케이션을 수정하기 어렵게 만든다.
- 객치지향 디자인은 **의존성을 관리하는 것**이고, 객체가 변화를 받아들일 수 있도록 의존성을 정리하는 코딩 기술의 묶음이다.
- 디자인이 결여되어 있을 때, 객체가 서로에 대해 너무 많이 알고 있기 때문에 관리되지 않은 의존성은 재앙을 불러온다. 다시 사용하기 어렵고 테스트하기도 힘들며 중복되기도 쉽다.

#### 🎈 디자인의 실용적 정의
- 모든 애플리케이션은 코드의 묶음이고, 코드를 배치하는 것이 곧 **디자인**이다.
- 디자인의 어려움 중 하나는 모든 문제가 두 부분으로 구성되어 있다는 점이다. 오늘 완성해야 하는 기능을 구현하는 코드를 짜야하고, 동시에 냉ㄹ 쉽게 바꿀 수 있는 코드를 짜야한다.
- 실용적 디자인은 우리의 애플리케이션에 어떤 일이 벌어질지를 예측하는 것이 아니라, 단지 **언젠가 무언가는 변한다는 사실 그리고 지금은 무엇이 변경될지 알 수 없다는 사실을 받아들이는 것이다.**
- 디자인은 나중에 디자인할 수 있는 여지를 남겨 놓기 위한 것이고, 그 최종 목표는 **변화의 비용을 최소화하는 것이다.**

### 📚 디자인 도구들

#### 🎈 디자인 원칙들
- 디자인 원치을 뜻하는 **SOLID**는 객체지향 디자인의 잘 알려진 디자인 원칙 다섯 가지를 대변한다.
- **단일 책임**(**Single Responsibility**), **개방-폐쇄**(**Open-Closed**), **리스코프 치환**(**Liskov Substitution**), **인터페이스 분리**(**Interface Segregation**), **의존성 역전**(**Dependency Inversion**)이다.
- 데메테르 프로젝트에서 시작된 **데메테르의 원칙**(**Law of Demeter-LoD**)

#### 🎈 디자인 패턴
- 객체지향 디자인은 원칙뿐만 아니라 **패턴**을 갖고 있다.
- 책 **디자인 패턴**은 패턴이란 **객체지향 소프트웨어 디자인에서 명확한 문제를 처리하는 간단하고도 우아한 해결책**이라고 말한다. 이 패턴을 이용하면 우리의 디자인을 보다 유연하며 이해하기 쉽게 만들 수 있으며 모듈화하여 재사용할 수 있게 만들 수 있다.

### 📚 디자인하기

#### 🎈 디자인은 어떻게 실패하는가
- 소프트웨어 디자인이 실패하는 첫 번째 원인은 디자인 자체가 부족하기 때문이다. 처음부터 프로그래머가 디자인 지식이 거의 없었을 수 있다.
- 경험이 조금 더 있는 프로그래머라면 객체지향 디자인 기술에 대해 알고 있지만, 이 기술을 어떻게 적용해야 하는지 잘 알지 못한다. 이들은 좋은 의도로 지나치게 디자인하는 함정에 빠진다.
- 마지막으로, 디자인 작업과 프로그래밍 작업이 동떨어져 있을 때 디자인은 실패한다.

#### 🎈 언제 디자인을 해야 하나
- 객체지향 디자인은 코드를 손쉽게 수정하려며 코드를 어떻게 배치해야 할지에 관심을 갖는다.
- 애자일 작업방식은 **변화를 보장한다.** 그리고 코드를 수정할 수 있는 우리의 능력은 애플리케이션의 디자인에 달려있다. 잘 디자인된 코드를 작성할 수 없다면, 새로운 주기마다 매번 애플리케이션을 다시 작성해야 할 것이다.

#### 🎈 디자인 평가하기
- 우리의 코드가 객체지향 디자인을 얼마나 잘 따르고 있는지 평가해주는 수 많은 루비 젬도 있다.
- 이 측정 소프트웨어들은 소스 코드를 훑어보고 코드의 질을 측정하는 데 사용할 수 있는 요소들의 개수를 샌다.
- 객체지향 디자인 점수(OOD metrics)를 낮게 받는 코드는 의심할 여지없이 잘못 디자인된 것이다. 이런 코드는 수정하기 힘들어진다.
- 객체지향 디자인 점수는 잘못된 것을 올바른 방법으로 구현하고 있는 디자인을 가려내지 못한다.
- 소프트웨어 질을 측정하는 궁극적인 기준은 **주어진 시간 안에서 기능별 구현 비용**일 것이다.
- 우리의 목표는 기능별 구현 비용이 가장 낮은 소프트웨어를 개발하는 것이기 때문에, 디자인에 얼마나 시간과 돈을 쓸지 결정하기 위해서는 두 가지를 고려해야 한다.
- 첫째는 우리의 기술 수준이고 둘째는 우리에게 주어진 시간이다.

### 📚 객체지향 프로그래밍에 대한 간략한 소개
- 객체지향 애플리케이션은 객체와 객체가 서로 주고 받는 메시지로 구성되어 있다.

#### 🎈 객체지향적 언어들
- 클래스 기반의 객체지향 언어인 루비는 데이터와 행동을 절대 공존할 수 없는 서로 다른 영역에 분리시켜 놓지 않는다. 즉, **객체**(**object**)로 통합한다.
- 객체는 행동을 가지고 있고, 데이터를 가지고 있을 수도 있다. 이 데이터에 누가 접근할 수 있는지는 객체가 결정하고 객체는 메시지 전송을 통해 상대의 행동을 실행시킨다.
- 루비는 문자열 **데이터 타입**이 아니라 문자열 **객체**를 갖고 있다. 문자열에 사용할 수 있는 오퍼레이션은 언어의 문법에 정의되어 있는 것이 아니라, 문자열 객체 안에 포함되어 있다.
- 모든 문자열 객체는 자신의 데이터를 외부세계로부터 **캡슐화**(**encapsulates**)시켜 놓는다. 모든 객체는 자신의 데이터를 얼마나 공개할지 또는 얼마나 감추고 있을지를 스스로 결정한다.
- 문자열 객체가 자신의 오퍼레이션을 직접 관장하기 때문에 루비는 문자열 데이터 타입에 대해 특별히 알고 있어야 할 것이 없다.
- 루비 같은 클래스 기반 객체지향 언어는 **클래스**를 정의할 수 있고 클래스는 비슷한 객체를 만들기 위한 청사진을 제공한다. 또한 클래스는 **메서드**(**행동을 정의한 것**)와 **어트리뷰트**(**변수를 정의한 것**)를 정의한다.
- 메서드는 메시지에 반응해서 실행되고 여러 객체가 같은 이름의 메서드를 정의할 수 있으며, 전송된 메시지를 가지고 어느 객체의 메서드를 실행할 지 결정하는 것은 루비의 몫이다.
- 객체의 타입을 안다는 것은 그 객체가 어떻게 행동할지 예상할 수 있다는 것이다.

### 📚 요약
- 변화를 손쉽게 받아들이 수 있도록 코드를 배치하는 일, 이것이 디자인이다.
- 디자인에서 원칙과 패턴이 즁요한데 원칙을 올바르게 적용하고 적절한 패턴을 사용해서 수정하기 쉬운 애플리케이션은 만들었다고 확신할 수는 없다.
- 디자인에 투자한 시간으로 본전이라도 뽑으려면 디자인 이론을 이해하고 적절히 적용할 수 있어야 한다. 올바른 순간에 필요한 만큼 적용할 줄 알아야 한다.