---
layout: post
title:  python 크롤링(selenium 사용법과 기초)
date:   2020-11-02 15:08:00 +0000
description:  selenium 사용법과 기초
img: selenium.png
tags: [More]
author: begginer_
---

# python 크롤링(selenium 사용법과 기초)

---

# 🤔Selenium으로 크롤링

출처 : [https://l0o02.github.io/2018/06/12/python-crawling-selenium-1/](https://l0o02.github.io/2018/06/12/python-crawling-selenium-1/)

### 1. Selenium이란?

 Selenium은 자동화 테스트를 위해 여러가지 기능을 지원하며 다양한 언어에서도 사용이 가능하다. bautifulsoup은 element를 뽑아내는 것이 조금 더 직관적이고 빠르지만 javascript에 조건이 충족되어야만 얻을 수 있는 데이터에 접근하는 것에 한계가 있다.

그래서, 직접적으로 웹 사이트에 접근할 수 있게 해주는 Selenium을 사용해야 한다. Selenium을 사용하기 위해서는 새로운 환경에서 웹 브라우저를 대신해 줄 web driver가 필요하다. web driver 설치는 위에 출처에 들어가 Web Driver를 누르면 자동으로 설치 파일로 가진다. Selenium으로 자동화하여 웹 사이트를 탐험하면 된다.

### 2. Selenium 이해하기

pip 명령어를 사용해 Selenium을 설치해준다.

```python
pip install selenium
```

python 파일을 하나 만들고 아래 코드를 실행한다.

```python
from selenium import webdriver

path = "(Webdriver의 경로)"
driver = webdriver.Chrome(path)
```

실행하게 되면, 크롬 창이 켜진다. Selenium으로 제어하기 때문에, 크롬창에 자동화된 테스트 소프트웨어로 제어중이다.

```python
driver.get('https://www.naver.com')
```

맨 마지막줄에 입력하고 다시 실행해보면 네이버로 접속된다.

### 3. Selenium으로 검색

```python
from selenium import webdriver

path = "(Webdriver의 경로)"
driver = webdriver.Chrome(path)
driver.get("https://google.com/")
search_box =  driver.find_element_by_name("q")
search_box.send_keys("BEGGINER")
search_box.submit()
```

 위에 코드를 실행해보면 구글에서 검색 input에 BEGGINER를 입력하고 submit()으로 검색 버튼을 누른거다.