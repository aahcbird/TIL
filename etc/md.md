# Markdown 문법

## 헤더
```
# 이것은 <h1> 태그 입니다.
## 이것은 <h2> 태그 입니다.
### 이것은 <h6> 태그 입니다.
```

## 리스트
### Unordered 리스트
```
* 아이템 1
* 아이템 2
  * 아이템 2a
  * 아이템 2b
```
* 아이템 1
* 아이템 2
  * 아이템 2a
  * 아이템 2b

### Ordered 리스트
```
1. 아이템 1
1. 아이템 2
1. 아이템 3
    1. 아이템 3a
    1. 아이템 3b
```
1. 아이템 1
1. 아이템 2
1. 아이템 3
    1. 아이템 3a
    1. 아이템 3b

## 강조
```
*이 텍스트는 기울어집니다*

_이 텍스트도 기울어집니다_

**이 텍스트는 볼드처리 됩니다**

__이 텍스트도 볼드처리 됩니다__

**__결합하여 사용 가능합니다__**
```
*이 텍스트는 기울어집니다*

_이 텍스트도 기울어집니다_

**이 텍스트는 볼드처리 됩니다**

__이 텍스트도 볼드처리 됩니다__

**_결합하여 사용 가능합니다_**

## 링크
```
http://github.com  // 자동으로 링크됨

[Github](http://github.com)
```
http://github.com

[Github](http://github.com)

## 이미지
```
![Alt Text](url)  // 기본 포맷
![꽃게](rustacean-flat-happy.png)

<img src="rustacean-flat-happy.png" width="200">  // 크기를 조정하고 싶으면 markdown 대신에 html 태그를 사용할 수 있음
```
<img src="rustacean-flat-happy.png" width="200">

## 인용구
```
> 무언가를 시작하는 방법은 말하는 것을 멈추고, 행동하는 것이다.
```
> 무언가를 시작하는 방법은 말하는 것을 멈추고, 행동하는 것이다.

## 인라인 코드
```
`@Component`는 해당 클래스가 스프링에서 객체로 만들어서 관리하는 대상임을 명시하는 어노테이션 입니다.
```
`@Component`는 해당 클래스가 스프링에서 객체로 만들어서 관리하는 대상임을 명시하는 어노테이션 입니다.

# Github 전용 Markdown
작업 중..


- [x] @mentions, #refs, [links](), **formatting**, and <del>tags</del> supported
- [x] list syntax required (any unordered or ordered list supported)
- [x] this is a complete item
- [ ] this is an incomplete item
