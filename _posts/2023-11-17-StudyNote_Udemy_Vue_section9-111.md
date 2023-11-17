---
layout: single
title: (Vue.js) 전역 컴포넌트, 지역 컴포넌트
categories: 공부노트
tag: Vue.js
toc: true
toc_sticky: true
toc_label: 순간이동
sidebar:
    nav: "counts"
---

- - -

## 전역 컴포넌트, 지역 컴포넌트란?

#### 전역 컴포넌트
- Vue 앱 어느 곳에서나, 즉 어느 템플릿에서나 사용 할 수 있는 컴포넌트로 루트 어디든 사용가능한 컴포넌트

#### 지역 컴포넌트
- 특정 컴포넌트에서만 사용이 되는 유효한 범위의 컴포넌트

- - -

## 전역 컴포넌트 등록 후 호출하는 방법

루트에 있는 main.js 파일에 전역 컴포넌트로 등록 할 수 있다.

예를들어

```javascript
// main.js

import { createApp } from 'vue';

import App from './App.vue';
import BaseBadge from './components/BaseBadge.vue';

const app = createApp(App);

app.component('base-badge', BaseBadge);

app.mount('#app');
```

BaseBadge라는 컴포넌트를 전역 컴포넌트로 등록할 경우 위와 같이 main.js에 import를 한 후 app.component에 "base-badge”라는 이름으로 등록 할 수 있다.

이렇게 되면 전역 컴포넌트로 등록이 되어 앱 내의 모든 컴포넌트에 호출하여 사용이 가능하다.

예를들어 BadgeList.vue 컴포넌트에 호출하여 사용한다 했을때

```javascript
// BadgeList.vue

<template>
  <section>
    <h2>Available Badges</h2>
    <ul>
      <li>
        <base-badge type="admin" caption="ADMIN"></base-badge>
      </li>
      <li>
        <base-badge type="author" caption="AUTHOR"></base-badge>
      </li>
    </ul>
  </section>
</template>
```

base-badge라는 태그로 바로 호출하여 사용이 가능하다.

- - -
## 지역 컴포넌트로 등록 후 호출하는 방법

지역 컴포넌트는 전역 컴포넌트와 다르게 사용할 해당 컴포넌트에 직접 등록을 하게 된다.

예를들어 App.vue에서 지역 컴포넌트로 등록을 할 경우
```javascript
// App.vue
<script>
import TheHeader from "./components/TheHeader.vue";
import BadgeList from "./components/BadgeList.vue";
import UserInfo from "./components/UserInfo.vue";

export default {
  components: {
    'the-header' : TheHeader,
    'badge-list' : BadgeList,
    'user-info' : UserInfo
  },
```

TheHeader, BadgeList, UserInfo라는 이름으로 컴포넌트를 import하고 components오브젝트를 만들고 안에는 호출해서 사용하게 될 이름인 프로퍼티 이름과 import한 컴포넌트를 Key-value형식으로 등록한다. 

등록한 컴포넌트를 호출할때는 프로퍼티 이름을 태그형식으로 사용해 호출한다.
```javascript
// App.vue
<template>
  <div>
    <the-header></the-header>
    <badge-list></badge-list>
    <user-info
      :full-name="activeUser.name"
      :info-text="activeUser.description"
      :role="activeUser.role"
    ></user-info>
  </div>
</template>
```

이때 좀 더 간결하게 컴포넌트를 등록하고 호출할 수 있다.
```javascript
// App.vue
<script>
import TheHeader from "./components/TheHeader.vue";
import BadgeList from "./components/BadgeList.vue";
import UserInfo from "./components/UserInfo.vue";

export default {
  components: {
    TheHeader : TheHeader,
    BadgeList : BadgeList,
    UserInfo : UserInfo
  },
```

위처럼 import해왔던 이름을 그대로 다시 사용하여 프로퍼티 이름으로 사용 가능하다.

하지만 이마저도 생략이 가능하다.

```javascript
export default {
  components: {
    TheHeader,
    BadgeList,
    UserInfo
  },
```
아예 import해왔던 이름만 가져와 등록해도 정상적으로 작동한다.

그렇다면 호출할땐 어떻게 해야할까?
3가지 방법이 있다.
TheHeader 기준으로 하면

1.
```javascript
export default {
  components: {
    "the-header" : TheHeader
  },
```

```javascript
<the-header></the-header>
```
위와 같이 정한 이름 그대로 불러오면 된다.

2.
```javascript
export default {
  components: {
    TheHeader : TheHeader
  },
```

```javascript
<the-header></the-header>
<TheHeader />
```
위와 같이 두가지 방법이 둘 다 가능하다.
어떻게 등록했던 이름과 다른데 가능할까?

이유는 Vue자체에서 번역을 하여 자동으로 연결을 시켜준다고 한다.

3.
```javascript
export default {
  components: {
   TheHeader
  },
```

```javascript
<the-header></the-header>
<TheHeader></TheHeader>
<TheHeader />
```
3가지 방법 다 작동한다.

사실상 세번째가 제일 사용하기 편하다.
- - -
## 추가적으로 알게 된 내용

사실 이미 알고 있었어야 했던 내용이 아니였나 싶다.

이제라도 정리를 해서 머리속에 저장해두자

- TheHeader : 첫글자, 중간글자에 대문자를 넣는 표기법 => 파스칼 케이스
- the_header : 언더바( _ )를 글자 중간에 넣는 표기법 => 스네이크 케이스
- theHeader : 첫글자는 소문자로 하되 중간글자는 대문자를 넣는 표기법 => 카멜 케이스

카멜 케이스는 글자 모양이 낙타를 닮았다 하여 낙타의 영문인 카멜(Camel)을 이용하여 카멜 케이스가 되었다.
