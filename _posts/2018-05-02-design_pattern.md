---
layout: post
title: "Design Pattern"
categories: [S/W Engineering]
tags: [Design Pattern]
---

개인적으로는 디자인 패턴이 얼마나 유용한지 모르겠다. 설계를 하다보면 자연스럽게 떠올리는 개념들인데 거창하게 이름만 붙인 것 같고, 몇몇 패턴은 현실의 복잡한 문제를 풀기에는 크게 도움이 안되는 것 같다. 그래도 이해해 두면 나쁠 것은 없으니 정리 차원에서 UML로 한 번 그려봤다. 패턴 자체보다는 패턴이 도출된 과정이 재미있고 의미가 있는 것 같다.

- Abstract Factory

![](/media/posts/design_pattern/abstract_factory.svg)

- Builder

![](/media/posts/design_pattern/builder.svg)

- Factory Method

![](/media/posts/design_pattern/factory_method.svg)

- Prototype

![](/media/posts/design_pattern/prototype.svg)

- Adapter

![](/media/posts/design_pattern/adapter.svg)

- Bridge
  - 브릿지는 서로 다른 두 개를 연결하는 존재다. 그렇다면 왜 연결할까? 뭔가 함께 해야 할 일이 있기 때문이겠지. Linux와 Windows에서 동작해야 하는 어떤 GUI클래스를 구현한다고 해보자. GUI클래스는 Linux던 Windows던 일관된 인터페이스를 가져야 그걸 사용하는 Application의 이식성이 높아질 것이다. 그래서 보통 GUI클래스의 인터페이스를 정의하고, 그 인터페이스를 상속받아 Linux용 GUI클래스와 Windows용 GUI클래스를 각각 만들게 된다. 그런데 이 때 문제 발생. GUI클래스가 세분화 된다면? 예를 들어 어린이용 GUI클래스가 필요하고, 노인용 GUI클래스가 필요하다면? 각각에 대해 모두 Linux, Windows 버전을 만들어야 한다. 뭔가 잘못된 느낌이 든다. GUI클래스의 구현은 2가지를 포함하고 있다. 하나는 로직. 하나는 OS의존적인 동작. 로직 구현은 추상화된 인터페이스에 따라 구현되었으나, OS에 의존적인 동작은 아직 단순 구현에 머물러있다. 따라서 OS의존적인 동작을 추상화된 OS 클래스로 만들고, 그에 따라 각각(Linux/Windows) 구현한 후 두 구현을 브릿지로 연결한다. OS 클래스가 하위 Layer 개념이므로, GUI 클래스에서 OS 클래스의 구현 참조를 가지도록 하고, 필요에 따라 OS 클래스의 인터페이스를 호출하도록 하자. 참조가 브릿지인 셈. 이렇게 되면 로직의 분화는 GUI클래스가 담당하게 되고, OS의 분화는 OS 클래스가 담당하게 된다. 당연히 확장,수정,이식에 유리해진다.  
![](/media/posts/design_pattern/bridge.svg)

- Composite

![](/media/posts/design_pattern/composite.svg)

- Decorator

![](/media/posts/design_pattern/decorator.svg)

- Facade
- Flyweight
- Proxy

![](/media/posts/design_pattern/proxy.svg)

- Chain of Responsibility

![](/media/posts/design_pattern/chain_of_responsibility.svg)

- Interpreter
- Iterator
- Mediator
- Memento
- Observer
- State
- Strategy
- Template Method
- Visitor

![](/media/posts/design_pattern/visitor.svg)
