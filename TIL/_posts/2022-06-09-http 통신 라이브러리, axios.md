---
title: "JS의 http 통신 라이브러리, axios"
tags:
  - Vue.js
  - axios

permalink: /til/:year/:month/:day/:title/
toc: true
toc_sticky: true
comments: true
---

# 오늘 한 일

1박 2일 사내 워크숍으로 인해 til 작성 계획에 중대한 차질이 생겼다. 그래서 원래 밤에 작성하던 til을 낮에 미리 작성해서 push한다.
앞으로 이런 변수에 어떻게 대처해야할지 잠깐 고민해보았다.
너무 강박을 가지는 것도 별로 좋지 않은 것 같다. 중요한 건 꾸준함이고, 그걸 실천해나가는 과정이다.

# 오늘 배운 것

## JS의 http 통신 라이브러리, axios

### axios란?

뷰에서 권고하는 HTTP 통신 라이브러리는 액시오스(Axios)이다.
Promise 기반의 HTTP 통신 라이브러리이며 상대적으로 다른 HTTP 통신 라이브러리들에 비해 문서화가 잘되어 있고
API가 다양해서 많이 쓰인다.

### 엑시오스 설치(CDN 방식)

```javascript
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```

### 엑시오스 사용 방법

라이브러리를 설치하고 나면 axios라는 변수에 접근할 수 있게 됩니다.
axios 변수를 이용하여 아래와 같이 HTTP GET 요청을 날리는 코드를 작성합니다.

#### 템플릿 부분

```html
<div id="app">
  <button v-on:click="getData">get user</button>
  <div>{{users}}</div>
</div>
```

#### 스크립트 부분

```javascript
<script>
    new Vue({
      el: '#app',
      data: {
          users: []
      },
      methods: {
          getData: function (){

              let vm = this;

              axios.get('https://jsonplaceholder.typicode.com/users/')
                  .then(function (response) {
                      console.log(response.data);
                      // this.users = response.data;  // axios 호출 후 this는 실행 컨텍스트가 바뀐 상태이므로, vm을 바라보지 않는 상태다.
                      vm.users = response.data;
                  })

              // 실패 시
                  .catch(function (error){
                      console.log(error);
                  })
          }

      }
    })
  </script>
```

자세한 문법은 axios 공식 레포지토리에서 확인하자!(https://github.com/axios/axios)

# 내일 할 일

- 정보처리기사 실기 공부
- vue.js 학습
- spring 복습
