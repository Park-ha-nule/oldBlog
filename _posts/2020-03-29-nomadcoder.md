---
layout: post
title:  nomadcoder 강의
date:   2020-03-29 21:05:00 +0000
description: nomadcoder 강의들으면서 개인 공부
img: nomadcoder.jpg
tags: [More]
author: begginer_
---

# nomadcoder

Created: Dec 26, 2019 3:17 PM
Property: MDN, flatuicolor
Regdt: 2020/01/03 → 2020/01/09
Reviewed: No
Type: JavaScript
text: nomadcoder

- 순서
    1. 변수 생성
    2. 초기화
    3. 사용
- let과 const의 차이

    let은 변수가 바뀌는 것을 허용한다
    const는 상수임(변수가 변하는 걸 허용하지 않음)

    변수 선언 할 때 되도록이면 const를 사용하는 걸 권장함
    나중에 충돌이 발생하지 않기 위해서

- 정렬하는 방법 2가지
    1. array
    : 데이터를 저장하는 곳(리스트 같이 저장함)
    2. object
    : value 이름을 설정할 수 있음(이게 key값이 됨)

        const hanuleInfo{
        	name:"hanule",
        	age : 21;
        }

- 언제 array를 쓰고 언제 object를 쓰는가?

    DB에 있는 리스트 데이터라면 array를 쓰고, 데이터를 합쳐서 만들어야 한다면 object를 사용함

    array를 object안에 쓸 수 있고, object를 array안에서도 쓸 수 있음

- 함수를 바로 호출하는 방법과 호출하고 싶을 때 호출하는 방법

    바로 : window.addEventListener("resize", 함수());

    나중에 : window.addEventListener("resize", 함수);

    이런건 언제 쓰냐?
    윈도우 사이즈가 변경될 때 이 함수를 실행해라 이럴 때 사용함

- 온라인, 오프라인 함수

        function online() {
        	console.log("인터넷 연결에 성공했습니다.");
        }
        function offline() {
        	console.log("인터넷 연결에 실패했습니다.");
        }
        
        window.addEventListener("online", online);
        window.addEventListener("offline", offline);

- Element.classList

    ***Element.classList***는 엘리먼트 클래스 속성의 컬렉션인 활성 DOMTokenList를 반환하는 읽기 전용 프로퍼티이다.
    clssList 사용은 공백으로 구분된 문자열인 `element.className`을 통해 엘리먼트의 클래스 목록에 접근하는 방식을 대체하는 간편한 방법이다.

    element.classList 자체는 읽기 전용이지만 메소드를 이용하여 변형할 수 있다.

    - 메서드
        1. add()
        : 지정한 클래스 값을 추가
        2. remove()
        : 지정한 클래스 값을 제거
        3. item(index)
        : 콜렉션의 인덱스를 이용하여 클래스 값을 반환함
        4. ***toggle***( String [ , force] )
        : 하나의 인수만 있을 때 : 클래스 값을 토글링한다.
        즉, 클래스가 존재한다면 제거하고 false를 반환하며, 존재하지 않으면 클래스를 추가하고 true를 반환한다.

            두 번째 인수가 있을 때 : 두번째 인수가 true로 평가되면 지정한 클래스 값을 추가하고 false로 평가되면 제거한다.

                //toggle을 사용하지 않을 때
                function clickTitle() {
                	const hasClss = title.classList.contains(clicked_class);
                	if(hasClass){
                		title.classList.remove(clicked_class);
                	} else {
                		title.classLsit.add(clicked_class);
                	}
                }
                //toggle 사용 시
                function clickTitle() {
                	title.classList.toggle(clicked_class);
                }

        5. contains()
        : 지정한 클래스 값이 엘리먼트의 class속성에 존재하는지 확인한다
        6. replace()
        : 존재하는 클래스를 새로운 클래스로 교체
- 오늘 배운거

        //html, css, js 분리
        /*
        1. html에 class = "btn"추가
        2. css에 가서 
        .btn {
        	cursor:pointer;
        }
        h1{
        	color : originalColor(원래 색상);
        }
        .clicked {
        	color : changeColor(바꿀 색상);
        	transition : color 0.5s ease-in-out;
        }
        3. js에 가서
        */
        //1번 경우
        const title = document.querySelector("#title");
        
        const clicked_class = "clicked";
        
        function clickTitle() {
        	const currentClass = title.className;
        	if(currentClass !== clicked_class){
        		title.className = clicked_class;
        	} else {
        		title.className = "";
        	}
        }
        
        function init(){
        	title.addEventListener("click", clickTitle);
        }
        
        init();
        //위에서의 문제점은 아예 bnt클래스 속성이 사라지게 됨 
        //이 문제를 해결하기 위한 방법이 2번 방법임
        const title = document.querySelector("#title");
        
        const clicked_class = "clicked";
        
        function clickTitle() {
        	const hasClass= title.classList.contains(clicked_class);
        	if(hasClass){
        		title.classList.remove(clicked_class);
        	} else {
        		title.classList.add(clicked_class);
        	}
        }
        
        function init(){
        	title.addEventListener("click", clickTitle);
        }
        
        init();
        
        //위에 방법을 더 간단히 하면 3번 방법임
        const title = document.querySelector("#title");
        
        const clicked_class = "clicked";
        
        function clickTitle() {
        	title.classList.toggle(clicked_class);
        }
        
        function init(){
        	title.addEventListener("click", clickTitle);
        }
        
        init();

---

### 시계

- 시계

        const clockTitle = document.getquerySelector("h1");
        
        function getTime(){
        	const date = new Date();
        	const hours = date.getHours();
        	const minutes = date.getMinutes();
        	clockTitle.innerText = `${hours}:${minutes}`;
        }
        
        getTime();

- setInterval, setTimeout 함수
    1. setInterval 함수
    : 일정한 시간 간격으로 작업을 수행하기 위해서 사용한다.
    `clearInterval` 함수를 사용하여 중지할 수 있다.
    주의할 점은 일정한 시간 간격으로 실행되는 작업이 그 시간 간격보다 오래걸릴 경우 문제가 발생할 수 있다.

        setInterval(함수, 시간 간격)

    2. setTimeout 함수
    : 일정한 시간 후에 작업을 한번 실행한다.
    기본적으로 setInterval 과는 달리 지정된 시간을 기다린 후 작업을 수행하고, 다시 일정한 시간을 기다린 후 작업을 수행하는 방식이다.
    `clearTimeout()`을 사용해서 작업을 중지할 수 있다.

위에 함수는 실시간으로 시계가 돌아가는걸 보기 위해 사용할 수 있음

    function init(){
    	getTime();
    	setInterval(getTime, 1000);
    }
    
    init();

- 위에서의 문제점 해결 방법

    위에서는 10보다 작은 수가 있으면 01, 02처럼 되는것이 아니라 그냥 1, 2 이렇게 나옴
    이걸 해결하는 방법은

        clockTitle.innerText = `${hours < 10 ? 0`${hours}` : hours} : ${minutes < 10 ? `0${minutes}` : minutes} : ${seconds < 10 ? `0${seconds}` : seconds}`;

- localStorage

    : 작은 정보를 유저 컴퓨터에 저장하는 방법

    읽기 전용 `localStorage` 속성은 사용자 로컬의 Storage 객체에 접근하게 해준다.
    `localStorage`는 `sessionStorage`와 비슷한데 차이점으로는 `localStorage`에 저장된 데이터는 만료 기간이 없지만 `sessionStorage`에 저장된 데이터는 세션이 끝나면 지워진다는 것이다.

    ---

    - ex
        1. 사용자 현재 도메인의 로컬 Storage 객체에 접근해 `Storage.setItem()`을 사용하여 데이터를 추가하는 코드다.

                localStorage.setItem('key', 'value');

            - localStorage 아이템 읽기

                    var cat = localStorage.getItem('key 값');

            - localStorage 아이템 삭제

                    localStorage.removeItem('value');

            - localStorage 아이템 전체 삭제

                    localStorage.clear();

    - 특징

        : localStorage에는 자바스크립트의 data를 저장할 수가 없다.

        오직 string만 저장할 수 있다.

- event.preventDefault & event.target

    : 이벤트를 취소할 수 있는 경우, 이벤트의 전파를 막지 않고 그 이벤트를 취소한다.
    `event.preventDefault()`

    이 경우는 submit을 할 때 한 페이지에서 문구만 바꾸고 싶을 때 주로 사용한다.

    event.target
    : 이벤트 객체를 받아온다.

---

### 이름 물어보고 이름 값 받아서 응용하기

- 오늘 배운것(이름 물어보고 그 이름 값 받아서 응용하기)

        <form class = "askname">
        	<input type = "text" placeholder = "what is your name?">
        </form>
        <h4 class = "result"></h4>

        .askname, result{
        	diplay:none;
        }
        .showing{
        	display:block;
        }

        const form = document.querySelector("askname"),
        	input = form.querySelector("input"),
        	result = document.querySelector("result");
        
        const current_user = "currentUser";
        const showing = "showing";
        
        function askname(){
        	const currentValue = localStorage.getItem(current_user);
        	//이 말은 currentValue에 current_user = currentUser라는 키 값의 value를 넣겠다.
        	if(currentValue === null){
        		askname2();
        	} else {
        		getName(currentValue);
        	}
        }
        
        function askname2(){
        	form.classList.add(showing);
        	form.addEventListener("submit", submitHandle);
        }
        
        function submitHandle(event){
        	event.preventDefault();
        	const currentValue = input.value;
        	getName(currentValue);
        	saveName(currentValue);
        }
        
        function getName(text){
        	result.classList.add(showing);
        	form.classList.remove(showing);
        	result.innerText = `Hello ${text}`;
        }
        //위에까지만 진행하면 새로고침할 시에 이름을 저장하지 못함 그래서 밑에 거를 추가해야 함
        function saveName(text){
        	localStorage.setItem(current_user, text);
        }
        
        getName();

JSON : Java Script Object Notation
데이터를 전달할 때, 자바스크립트가 그걸 다룰 수 있도록 object로 바꿔주는 기능
자바스크립트의 object를 string으로 string을 object로 바꿀 수 있다.

- JSON.stringify(), JSON.parse()
    1. `JSON.stringify(value[, replacer[, space]])`
    : JavaScript 값이나 객체를 JSON 문자열로 변환한다.
    object를 string으로 바꿔준다.
    선택적으로 replacer를 함수로 전달할 경우 변환 전 값을 변형할 수 있고, 배열로 전달할 경우 지정한 속성만 결과에 포함된다.
        - value : JSON 문자열로 변환할 값
        - replacer : 문자열화 동작 방식을 변경하는 함수, 혹은 JSON 문자열에 포함 될 값 객체의 속성들을 선택하기 위한 화이트리스트로 쓰이는 `STRING`과 `NUMBER` 객체들의 배열
        - space : 가독성을 목적으로 JSON문자열 출력에 공백을 삽입하는데 사용되는 `string` 또는 `number`객체
    2. `JSON.parse(text[, reviver])`
    : object 형식으로 변환 된다.
        - text : JSON으로 변환할 문자열을 의미한다.
        - reviver : 함수라면, 변환 결과를반환하기 전에 이 인수에 전달해 변형한다.
- console.dir, time, timeEnd
    - dir(object)
    : 자바스크립트 객체의 속성들을 출력
    - time(id)
    : 실행 시간을 측정하기 위한 시작 시간을 기록
    - timeEnd(id)
    : 실행 시간을 측정하기 위한 끝 시간을 기록
- **forEach, filter()**
    1. `forEach`
    : 기본적으로 함수를 실행시키는 건데, array에 담겨있는 것들을 각각에 한번씩 함수를 실행시켜 주는 것이다.

        forEach는 array를 위한 함수이다.

    2. `filter()`

        : 주어진 함수의 테스트를 통과하는 모든 요소를 모아 새로운 배열로 반환한다.

            const words = ['spray', 'watermelon'];
            const result = words.filter(word => word.length > 6);
            console.log(result);

---

### todoList 생성

- todoList 생성

        /*html
        <form class = "todoForm">
        	<input type = "text" placeholder = "Write a to do">
        </form>
        <ul class = "todoList"></ul>
        */
        
        /*javascript*/
        const todoForm = document.querySelector(".todoForm"),
        	input = todoForm.querySelector("input"),
        	todoList = document.querySelector(".todoList");
        
        const LS = "todos";
        
        let todoArr = [];
        
        function init(){
        	loadToDo();
        	todoForm.addEventListener("submit", handleSumbit);
        }
        
        function loadToDo() {
        	const loadedToDo = localStorage.getItem(LS);
        	if(loadedToDo !== null) {
        		const parseToDo = JSON.parse(loadedToDo);
        		parseToDo.forEach(function(todo){
        			filltodo(todo.text);
        		});
        	}
        }
        
        function handleSubmit(event){
        	event.preventDefault();
        	const currentValue = input.value;
        	filltodo(currentValue);
        	input.value = "":
        }
        
        function deleteToDo(event){
        	const btn = event.target;
        	const li = btn.parentNode;
        	todoList.removeChild(li);
        	//새로고침 문제를 해결
        	const cleanToDo = todoArr.filter(function(todo) {
        		return todo.id !== parseInt(li.id);
        	});
        	todoArr = cleanToDo;
        	saveToDo();
        }
        
        function filltodo(text){
        	const li = document.createElement("li");
        	const deleteBtn = document.createElement("button");
        	const span = document.createElement("span");
        	deleteBtn.innerText = "X";
        	deleteBtn.addEventListener("click", deleteToDo);
        	span.innerText = text;
        	li.appendChild(deleteBtn);
        	li.appendChild(span);
        	todoList.appendChild(li);
        	const newId = todoArr.length + 1;
        	const todoObj = {
        		text : text,
        		id : newId
        	}
        	todoArr.push(todoObj);
        	saveToDo();
        }
        
        function saveToDo(){
        	localStorage.setItem(LS, JSON.stringify(todos)); 
        	// localStorage는 오직 string만 저장 가능하다.
        }

- Math.floor & Math.ceil
    1. Math.floor
    : 내림
    2. Math.ceil
    : 올림
- .prepend() & z-index(css)

    : 선택한 요소의 내용의 앞에 콘텐트를 추가한다.
    `.prepend( content [ ,  content  ] )`

        <p>Lorem Ipsum Dolor</p>
        $('p').prepend('123');
        <p>123 Lorem Ipsum Dolor</p>

    ---

    z-index
    : position 속성을 이용하면 요소를 겹치게 놓을 수 있다.
    이때 요소들의 수직 위치를 z-index 속성으로 정한다.
    값은 정수이며, 숫자가 클 수록 위로 올라오고, 숫자가 작을 수록 아래로 내려간다.

---

### 랜덤으로 배경 이미지 바꾸기

[배경 넣기 예제](https://www.notion.so/de1760715cac49d8a65731df3f677b8f)

- API에서 image따올 때 필요한 것

        image.addEventListener("loadend", handleImgLoad);
        
        function handle.imageLoad() {
        	console.log("finished loading");
        }

---

### 날씨 정보 받아오기

[Geolocation API](https://www.notion.so/Geolocation-API-d5e35f36305646c1b3f924d4b5d6763e)

- API(Application Programming Interface)

    : 다른 서버로부터 손쉽게 데이터를 가져올 수 있는 수단이다.

    [https://home.openweathermap.org/api_keys](https://home.openweathermap.org/api_keys) (open API 받아올 수 있는 곳)_naver이메일

- network 패널

    : 우리가 request한 내용을 보여준다.(api, css, js등등)

[API를 이용한 위치정보 예제](https://www.notion.so/API-db9a7e8f88c64448bac1b4a6f3624170)