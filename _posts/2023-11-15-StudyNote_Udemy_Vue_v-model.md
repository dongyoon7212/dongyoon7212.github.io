---
layout: single
title: (Vue.js) v-model란?
categories: 공부노트
tag: Vue.js
toc: true
toc_sticky: true
toc_label: 순간이동
sidebar:
    nav: "counts"
---

# (Vue.js) v-model

- - -

## v-model 이란?

쉽게 말해 v-bind와 v-on을 합친 것이라고 생각하면 된다.
입력을 통한 데이터 속성을 전달하고 동시에 이벤트를 수행한다.

기본적으로 사용법은 이러하다.
```javascript
<input v-model="searchText" />
```

이것을 v-bind와 v-on로 풀어서 코드를 쓰면
```javascript
<input
  :value="searchText"
  @input="searchText = $event.target.value"
/>
```

프로젝트에 적용해보자
```javascript
<template>
  <form @submit.prevent="submitData">
    <div>
      <label>Name</label>
      <input type="text" v-model="enteredName" />
    </div>
    <div>
      <label>Phone</label>
      <input type="tel" v-model="enteredTel" />
    </div>
    <div>
      <label>E-Mail</label>
      <input type="email" v-model="enteredEmail" />
    </div>
    <div>
      <button>Add Contact</button>
    </div>
  </form>
</template>
```

이름, 전화번호. 이메일을 입력받는 요소를 만들었다.

여기서 입력받은 데이터들을 저장해두기 위해 data함수를 이용한다.
```javascript
data() {
    return {
      enteredName: "",
      enteredTel: "",
      enteredEmail: "",
    };
  },
```

entered~로 입력받은 데이터들을 저장하고 v-model로 넘겨준다.
이렇게 하면 입력받은 값들을 양방향 바인딩 하면서 이벤트에 같이 사용이 가능하다.
