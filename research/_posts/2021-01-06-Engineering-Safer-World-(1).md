---
layout: post
title: Engineering Safer World (1)
category: research
tags: safety
sitemap: false
---

Nancy G. Leveson 교수님의 [Engineering a Safer World](https://direct.mit.edu/books/book/2908/Engineering-a-Safer-WorldSystems-Thinking-Applied)

첫번째는 왜 새로운 Safety Approach가 필요한가에 대한 설명이다.
이 글은 해당 책의
```
1. Why Do We Need Something Different
2. Questioning the Foundations of Traditional Safety Engineering
```
이 두 챕터 내용을 담는다.


## 왜 새로운 Safety Analysis Method가 필요한가?
저자는 기존 approach들이 이전에는 잘 적용되어 왔지만, 현대의 시스템에 적용하기에 부족한 부분이 있다고 말한다.

저자가 제시한 문제점은 총 9가지이며, 공통된 맥락에서 이어지지만, 굳이 분류하자면 두 가지 카테고리로 나뉘어진다.

### 기술의 발전
기술이 발전하는 속도는 점차 빨라지고 있다. 지난 100년에서 일어난 과학기술의 발전이 그 전 100만년동안 발전해왔던 과학 기술보다도 많다고 한다.[^1]

특히 주목해야할 것은 기술이 발전된 순간부터 실제로 상용화되기까지의 시간이 매우 짧아졌다는 것이다.
이 시간이 짧아짐으로서, 새로운 기술을 시스템에 적용해서 testing 하거나, 잠재적인 risk를 파악할 수 있는 시간과 능력이 줄어들었다.

발전된 기술을 시스템에 접목시키면서 생기는 큰 변화 중 하나는 새로운 형태의 사고, Risk, Hazard를 발생시킨다는 것이다.

Watchdogs 시리즈는 도시 거의 대부분의 요소들이 ctOS라는 도시 관리 클라우드에 연결되어 있는 사회가 배경인 게임이다.
이 게임의 주 특징은 신호등, 배관, 차, 등 모든 요소들을 *해킹*을 통해 내 마음대로 조작할 수 있다는 것이다.
iOT의 발전으로 시스템이 인터넷에 연결되면서 보안과 관련된 새로운 사고, Risk, Hazard가 생겨난 것이다.


### 시스템의 변화
복잡도가 높고, 규모가 큰 시스템이 많아진 것도 하나의 문제점이다.

Fault Tree Analysis와 같이 간단하게 어떤 문제가 몇몇 component의 failure로 나타난다고 말하기 어려울 정도로 component간의 interaction이 늘어나고, 시스템이 dynamic 해졌다.
또한, component 각각에서 볼 수 없었던 창발적 특성, emergent behavior가 나타나면서, 모든 요소들을 이해하고, 관리할 수 있는 사람이 있는 것은 매우 어려워졌다.

또한 이런 시스템 한 번의 failure로 나타나는 파급효과가 점점 커지고 있다.
규모가 큰 시스템, 사회 자본이 많이 투자된 시스템일 수록 복잡성은 높아지고, failure로 나오는 경제적인 손실은 증가하고 있다.

이런 시스템을 효과적으로 관리하기위해 다양한 Automation 기법들이 발전되어왔고, 사용되고 있다.
4차 산업혁명이 진행되는 것처럼 사람은 점점 higher-level decision만을 하고, 대부분의 일은 automation이 주로 하게 될 것이다.
따라서 인간-기계간의 상호작용에서의 실수, 부적절한 의사소통도 Fault Tree Analysis와 같은 고전적 방법에서 분석할 수 없지만, Safety에 필수적인 요소로 새롭게 등장했다.

또한, 이런 높은 복잡도와 대규모 시스템은 한 개인이 아니라 국가 차원에서의 규제와 관리가 동반되고 있다.
따라서, 사회적인 분석도 함께 진행되어야 한다.

***
## 새로운 Method는 무엇이 달라져야 하는가?

이런 패러다임의 변화는 고전적 분석 방법에서 사용되던 assumption이 더 이상 통용되지 않는다는 것을 의미한다.
저자는 새로운 분석 방법에서 사용되는 assumption을 고전적 분석의 assumption과 비교해서 설명하고 있다.

### Safety와 Reliability

> Safety는 System 혹은 component의 Reliability가 증가하면 증가한다.
> 만약, component 혹은 system의 failure가 일어나지 않는다면, 사고는 일어나지 않는다.
> 
> Reliability가 높은 software는 안전하다.

System Reliability라고 함은 특정 Requirement대로 시스템이 제대로 작동하는 것을 의미한다.
Requirement대로 시스템이 정확하게 설계되고, 구현되었더라도, Safety가 충족되었는 지는 확인할 수 없다.
각 component간의 interaction에서 failure가 발생할 수 있기 때문이다.[^2]

> Reliability는 Safety와 연관 관계가 없다.
> 
> Software의 Reliability가 높다고 해서 안전하다는 보장은 없다.
> Software의 Reliability를 높이는 것은 safety에 매우 적은 영향만을 줄 뿐이다.

* Event Chain

> 사고는 직접적으로 연관된 event chain에 의해서 일어난다.
> Event chain을 통해서, 사고를 분석하거나, Risk를 분석할 수 있다.
> 
> Event chain의 확률을 통한 Risk 분석은 Risk를 분석하는 좋은 방법이다.
> 
> 대형 사고는 랜덤한 event들이 동시에 일어나서 발생한다.


> 사고는 사회적, 기술적인 상호작용이 포함된 시스템에서 복잡한 과정을 거쳐 일어난다.
> 기존의 Event chain은 이 과정을 잘 묘사할 수 없다.
> 
> Risk와 Safety는 확률적인 분석으로는 분석할 수 없다.
> 
> 시스템은 시간이 지날 수록 점차 risk가 높은 state로 이동한다.
> 이러한 이동은 적절한 system design을 통해 예측할 수 있거나, 감지될 수 있다.

* Operator Error

> 대부분의 사고는 Operator Error에서 발생한다.
> Safe한 행동을 칭찬하고, Unsafe한 행동에 징계를 주는 것이 사고 예방에 도움이 된다.
> 
> 책임 소재가 누구인지 판단하는 것이 다음 사고 예방에 도움이 된다.
    
> Operator Error는 그 환경에서 자연스럽게 만들어진다.
> Operator "error"를 줄이기 위해서는, operator가 일하는 환경을 개선해야 한다.
> 
> 책임 소재가 누구인지 찾는 것은 Safety에 악영향을 끼칠 뿐이다.
> 사람 혹은 특정 component의 책임 소재를 찾는 것보다 시스템의 behavior를 전체적으로 바라보아야 한다.
***

***
[^1]: 곽영직. _인류 문명과 함께 보는 과학의 역사_. 세창출판사, 2020. 당연히 엄밀한 이야기는 아니겠지만, 다들 공감하는 내용일 것이다.

[^2]: Mars Polar Lander 사고가 바로 이러한 케이스다. 