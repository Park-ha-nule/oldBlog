---
layout: post
title:  kakao login
date:   2020-06-02 23:39:00 +0000
description: springboot kakao login
img: kakao.png
tags: [More]
author: begginer_
---

# kakao 계정으로 로그인

---

 카카오 계정으로 로그인을 프로젝트에 넣으려면 **kakao developers**에서 프로젝트를 등록해야함

- 순서
    - 앱 등록 정보로 카카오 로그인 페이지 띄움
    - 로그인 완료 시 앱 연동 화면이 나오고 동의를 통해 앱과 카카오 계정 연결
    - 앱에 설정한 콜백 페이지가 인증 코드와 함께 호출
    - 전달된 콜백 페이지에서 인증코드로 token을 얻어 화면에 표시
- 1. 카카오 로그인 및 콜백 페이지 연동

    : 카카오와 통신이 필요함으로 SpringRestApiApplication에 RestTemplate Bean을 추가

    ```java
    @SpringBootApplication
    public class SpringRestApiApplication {
    	public static void main(String[] args) {
    		SpringApplication.run(SpringRestApiApplication.class, args);
    	}

    	@Bean
    	public PasswordEncoder passwordEncoder() {
    		return PasswordEncoderFactories.createDelegationPasswordEncoder();
    	}
    	
    	@Bean
    	public RestTemplate restTemplate() {
    		return new RestTemplate();
    	}
    }
    ```

- 2. build.gradle에 라이브러리 추가
: 카카오 연동 시 결과 Json을 객체로 맵핑하기 위해 Gson 라이브러리 사용

    ```java
    implementation 'com.google.code.gson:gson'
    ```

- 3. kakao api와 연동하기 위한 설정 정보를 application.yml에 추가

    ```java
    //나는 application.properties에 추가했다.
    social.kakao.client_id : xxxxxxx # 앱 생성시 받은 REST API 키
    social.kakao.redirect: /social/login/kakao
    social.kakao.url.login: https://kauth.kakao.com/oauth/authorize
    social.kakao.url.token: https://kauth.kakao.com/oauth/token
    social.kakao.url.profile: https://kauth.kakao.com/v2/user/me
    url.base: http://localhost:8080
    ```

- 4. /social/login/kakao 화면은 카카오 로그인 팝업을 띄우기 위해 버튼만 존재한다. 카카오 로그인 화면을 띄우려면 다음과 같은 형식으로 호출해야한다.

    ```java
    package com.rest.api.controller.common;

    // import 생략

    @RequiredArgsConstructor
    @Controller
    @RequestMapping("/social/login")
    public class SocialController {

        private final Environment env;
        private final RestTemplate restTemplate;
        private final Gson gson;
        private final KakaoService kakaoService;

        @Value("${spring.url.base}")
        private String baseUrl;

        @Value("${spring.social.kakao.client_id}")
        private String kakaoClientId;

        @Value("${spring.social.kakao.redirect}")
        private String kakaoRedirect;

        /**
         * 카카오 로그인 페이지
         */
        @GetMapping
        public ModelAndView socialLogin(ModelAndView mav) {

            StringBuilder loginUrl = new StringBuilder()
                    .append(env.getProperty("spring.social.kakao.url.login"))
                    .append("?client_id=").append(kakaoClientId)
                    .append("&response_type=code")
                    .append("&redirect_uri=").append(baseUrl).append(kakaoRedirect);

            mav.addObject("loginUrl", loginUrl);
            mav.setViewName("social/login");
            return mav;
        }

        /**
         * 카카오 인증 완료 후 리다이렉트 화면
         */
        @GetMapping(value = "/kakao")
        public ModelAndView redirectKakao(ModelAndView mav, @RequestParam String code) {
            mav.addObject("authInfo", kakaoService.getKakaoTokenInfo(code));
            mav.setViewName("social/redirectKakao");
            return mav;
        }
    }
    ```

- 5. 카카오 token api 연동시 맵핑을 위한 모델 생성

    ```java
    package com.rest.api.model.social;

    import lombok.Getter;
    import lombok.Setter;

    @Getter
    @Setter
    public class RetKakaoAuth {
        private String access_token;
        private String token_type;
        private String refresh_token;
        private long expires_in;
        private String scope;
    }
    ```

- 6. 카카오 로그인 페이지 작성
: 로그인 화면에서는 KakaoLogin버튼을 누르면 서버에서 전달받은 URL을 팝업으로 띄우는 코드로만 이루어져있다. 카카오 로그인 팝업이 열리고 로그인 후에는 앱을 연동하지 않은 경우에는 연동 화면이 나온다.

    ```java
    <button onclick="popupKakaoLogin()">KakaoLogin</button>
    <script>
    	function popupKakaoLogin() {
    		window.open('${loginUrl}', 'popupKakaoLogin',
    'width=700, height=500, scrollbars=0, toolbar=0, menubar=no')
    	}
    </script>
    ```
