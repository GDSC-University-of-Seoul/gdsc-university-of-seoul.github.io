---
layout: post
title: "서버 없이 데이터를 저장하고 싶어요!"
authors: [baebae02]
tags: ["web", "웹 스토리지", "클라이언트"]
image: ../assets/images/post-save-data-without-server/1.jpg
featured: true
---

# 서버 없이 데이터를 저장하고 싶어요!

웹 개발을 하다 보면 정보를 기억해야 하는 순간이 꼭 옵니다. 회원가입 시 입력한 개인정보뿐만 아니라 이전 페이지에서 무엇을 체크했는지와 같은 사소한 선택지도 있겠죠?

<aside>
❓ 이러한 데이터를 저장하려면 꼭 데이터베이스와 서버가 필요 할까요?

</aside>

정답은 **“아니다”** 입니다!

우리는 **웹 브라우저에서 제공하는 db를** 사용해 데이터를 저장할 수 있어요. 브라우저의 db를 사용할 수 있는 방법엔 “IndexedDB, Cookies, Web storage(Local, Session)”등이 있습니다.

<aside>
💡 IndexedDB, Cookies, Web storage(Local, Session)를 통해 브라우저에 데이터 저장 가능

</aside>

오늘은 위에서 언급한 **4가지 방법**을 모두 다루려고 합니다!

![image](../assets/images/post-save-data-without-server/1.jpg)

## WebStorage

웹 스토리지는 웹 개발을 한다면 한 번쯤은 사용하게 될 친구입니다. **Local Storage, Session Storage** 두 가지가 있는데, 이 둘의 차이는 **'무엇을 기준으로 저장되느냐?’**에 있습니다.

### Local Storage

로컬 스토리지는 창, 즉 브라우저를 기준으로 저장됩니다. **한 브라우저당 하나의 Local Storage**을 가집니다. 만약 내가 한 창안에서 여러 탭을 띄웠다면 이 탭들은 같은 Local Storage를 공유합니다. 그래서 한 탭에서 다른 탭으로 이동해도 Local Storage에 저장된 데이터는 사라지지 않습니다. 하지만 사파리와 크롬을 하나씩 띄웠다면, 이 두 브라우저는 각각 다른 로컬 스토리지를 갖고 있겠죠?

Local Storage에 저장한 데이터를 지우려면 **JavaScript를 코드로 삭제하거나 브라우저의 캐시 또는 local Storage 데이터를 직접 지워야**합니다. 그 때문에 로그인이나 접속 이력 등을 관리할 때 편리합니다.


### Session Storage

세션 스토리지는 탭, 즉 세션을 기준으로 저장됩니다. 한 탭 당 하나의 Session Storage를 가집니다. 때문에 내가 탭을 이동하면 이동한 탭의 세션 스토리지는 이전 탭의 스토리지와 다릅니다!

Session Storage에 저장된 데이터는 탭 또는 창이 종료되면 자동으로 삭제됩니다. 이런 이유로 Local Storage보다 데이터 보존 시간이 짧다는 것입니다.

Session Storage는 수강신청 탭에서 세션만료를 체크할 때 사용하거나, 사용자가 '입력폼'을 입력하다가 페이지를 벗어난 경우 백업하기 위해 사용하기도 합니다. 

<aside>
💡 저장 공간은 Local Storage > Session Storage 입니다.

</aside>

### 사용법

```jsx
// 키에 데이터 쓰기
window.localStorage.setItem("key", value);
window.sessionStorage.setItem("key", value);

// 키로 부터 데이터 읽기
window.localStorage.getItem("key");
window.sessionStorage.getItem("key", value);

// 키의 데이터 삭제
window.localStorage.removeItem("key");
window.sessionStorage.removeItem("key", value);

// 모든 키의 데이터 삭제
window.localStorage.clear();
window.sessionStorage.clear();

// 저장된 키/값 쌍의 개수
window.localStorage.length;
window.sessionStorage.length;
```

### 예제(Local)

- F12를 눌러 개발자 도구에 들어간 상태에서, 콘솔창에 다음과 같이 쳐봅니다.
- 그런 다음 ‘Application’에 들어가줍니다.

![image](../assets/images/post-save-data-without-server/2.png)

![image](../assets/images/post-save-data-without-server/3.png)

- LocalStorage에 들어가 보면 value를 “gdsc”로 갖는 데이터가 저장되었음을 볼 수 있습니다.
- 이미 다른 데이터도 많이 저장되어 있죠? 제가 설치한 크롬 확장 프로그램에서 저장해 둔 데이터인 것 같습니다.
- **탭을 껐다 켜도 남아있어요. 한번 테스트해보세요!**
- Session Storage도 같은 방식으로 테스트할 수 있습니다.

### IndexedDB

다음으로는 IndexedDB입니다.

> IndexedDB는 관계형 데이터베이스(RDBMS)와 같이 트랜잭션을 사용하는 데이터베이스 시스템입니다. 그러나 IndexedDB는 RDBMS의 고정컬럼 테이블 대신 JavaScript 기반의 객체지향 데이터베이스입니다.
>

사용할 수 있는 웹 스토리지 중에서 제일 실제 데이터베이스와 비슷하달까요!

문자열 타입의 키&값을 사용해야 하는 webStorage와 달리 IndexedDB에서는 js가 취급하는 모든 타입을 사용할 수 있습니다. 여러개의 데이터베이스를 생성할 수 있으며, **데이터를 요청하고 응답받는 과정이 비동기적으로 작동한다**는 점이 특이사항입니다.

그 때문에 단순하고 적은 양의 데이터가 아닌, 많은 양의 구조화된 데이터를 쌓고 싶을 때 추천합니다 😎

## 사용순서

1. 데이터베이스 열기
2. 데이터베이스에 객체 저장소(*Object store*) 생성하기
3. 요청 보내기
   트랜잭션을 사용해서 보냄. (`readonly`, `readwrite`, `versionchange`)
4. 요청이 완료될 때까지 기다리기
5. 요청 결과를 가지고 어떤 동작하기

<aside>
❓ 트랜젝션이란 db의 상태를 변화시키기 위해 수행하는 작업 단위

</aside>

**예시코드**

```jsx
//1. 데이터베이스 열기
const idxedDB = window.indexedDB;
const request = idxedDB.open('SampleDB');

//2. 데이터베이스에 객체 저장소 생성하기
IDBRequest.createObjectStore('store_name', {keyPath: 'id'})

//3. 트랜젝션 사용하여 요청 보내기
IDBDatabase.transaction(store_names, mode, options);

//4. 이후 get, put, delete, create를 통해 데이터 수정 가능
const objStore = transaction.objectStore('name');
const request = objStore.add(name); //[POST]
const objStoreRequest = objStore.get(key); //[GET]
const updateRequest = objStore.put(value); //[PUT]
const objStoreRequest = objStore.delete(key); //[DELETE]
```

> **C(create), R(read), U(update), D(delete)**는 데이터베이스를 사용하기 위한 기초적인 4가지 쿼리 형식이며, 줄여서 **CRUD**라고 부른답니다!
indexedDB에서는 CRUD에 해당하는 메소드들이 **add, get, put, delete**로 정의되어 있어요 :)
>

# 총정리

|  | session storage       | local storage                       | indexedDB            |
| --- |-----------------------|-------------------------------------|----------------------|
| 용량 | 가장 적음                 | 보통                      | 가장 큼                 |
| 수명 | 탭이 닫히면, 세션이 만료되면 삭제 됨 | 코드를 통해서 삭제하거나 직접 삭제. 창이 꺼져도 삭제되지 않음 | 코드를 통해서 삭제하거나 직접 삭제. |
| 방식 | 동기                    | 동기                                  | 비동기                  |
| 형식 | 문자열 타입만 가능            | 문자열 타입만 가능                          | JS 자료형 가능            |
| 여러개의 데이터베이스 | X                     | X                                   | O                    |
| 난이도 | ⭐️                    | ⭐️                                  | ⭐️⭐️⭐️               |

<aside>
❓ web storage와 함께 쿠키 & 세션에 대한 개념도 같이 공부하시길 추천합니다 !

</aside>

[쿠키와 세션을 이용한 로그인 (feat. JWT)](https://gdsc-university-of-seoul.github.io/Login-using-cookie-and-session/)

### References

[브라우저 저장소 (Cookie, WebStorage,Indexed DB)](https://velog.io/@yebb/%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80-%EC%A0%80%EC%9E%A5%EC%86%8C-Cookie-WebStorageIndexed-DB)

[cool-dawn-szlel](https://codesandbox.io/s/cool-dawn-szlel?file=/src/App.vue)

[indexedDB에 대해 알아보자!](https://mong-blog.tistory.com/entry/indexedDB%EC%97%90-%EB%8C%80%ED%95%B4-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90)
