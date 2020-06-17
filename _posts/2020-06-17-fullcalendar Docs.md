---
layout: post
title:  fullcalendar Doc / Toolbar 번역
date:   2020-06-17 17:48:00 +0000
description: fullcalendar Doc / Toolbar 번역
img: toolbar.png
tags: [More]
author: begginer_
---

# Docs / Toolbar

---

- calendar의 top과 bottom의 버튼과 다른 컨트롤 부분

# header

---

- 캘린더의 윗부분의 버튼과 제목 정의

```jsx
Object/false, default:
{
	left : 'title',
	center : '',
	right : 'today prev,next'
}
```

 header의 설정을 false로 설정하면, header가 보이지 않을것이다. left, center, right의 속성을 제공한다. 이 속성들은 쉼표/공백으로 구분된 값들을 포함한다. 쉽표로 구분된 값은 적절하게 표시된다. 공백으로 구분된 값은 사이에 작은 간격이 표시된다. 문자열은 다음 값 중 하나를 포함할 수 있다 :

- title
    - 현재 달/주/날을 포함하는 문자
- prev
    - 달력을 한 달/주/일 뒤로 이동하기 위한 버튼
- next
    - 달력을 한 달/주/일 앞으로 이동하기 위한 버튼
- prevYear
    - 달력을 1년 뒤로 이동하기 위한 버튼
- nextYear
    - 달력을 1년 앞으로 이동하기 위한 버튼
- today
    - 현재 달/주/날로 이동하기 위한 버튼
- a view name
    - 달력을 사용 가능한 보기로 전환하는 버튼

속성이 빈값으로 명시되어 있다면 글/버튼이 보이지 않을 것이다.
<br><br><br>
---
# footer

---

달력의 맨 아래에 있는 컨트롤 정의

```jsx
Object / false (the default)
```

이 세팅은 header 옵션과 동일한 값을 허용한다.

이것은 기본적으로 거짓이며, 이것은 달력 밑에 컨트롤이 되지않는다는 것을 의미한다.
<br><br><br>
---
# titleFormat

---

header의 title을 표시한다.

```jsx
Date Formatter, default :
{ year: 'numeric', month: 'long'}
{ year: 'numeric', month: 'short', day: 'numeric'}
{ year: 'numeric', month: 'long', day: 'numeric'}
```

 위에서 언급한것과 같이, 각 화면에는 특정한 기본값이 존재한다. 화면-특정 옵션을 사용하여 세부 조정된 컨트롤을 가져와라. 단일 문자열로도 모든 화면의 값이 설정된다.

날짜 범위 텍스트를 표시하는 화면의 경우, 두 날짜 사이의 텍스트를 제어하려면 titleRangeSeparator을 사용자 정의해라.
<br><br><br>
---
# titleRangeSeparator

---

toolbar 제목에 날짜 범위를 포매팅할때 사용자를 정의한다.

```jsx
String, default : ' \u2013 '(en dash)
```

titleFormat과 함께 작업

모든 다른 날짜 범위 구분 문자 텍스트의 경우, defaultRangeSeparator를 사용해라
<br><br><br>
---
# buttonText

---

header/footer의 버튼에 있는 글씨

```jsx
Object, default:
{
	today : 'today',
	month : 'month',
	week : 'week',
	day : 'day',
	list : 'list'
}
```

 버튼아이콘과 bootstrapFontAwesome은 특정 다른 버튼의 모양에 영향을 미친다.

html 주사제는 제공하지 않는다. 모든 특수 문자는 escaped문자열을 쓴다.