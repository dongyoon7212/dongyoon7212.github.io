---
layout: single
title: (Vue.js) methods, emits
categories: 공부노트
tag: Vue.js
toc: true
toc_sticky: true
toc_label: 순간이동
sidebar:
    nav: "counts"
---

# (Vue.js) methods, emits

- - -

## methods란?

특정 기능을 수행하는 것들을 묶어놓는 함수를 뜻한다.
공식문서에 따른 타입은
```javascript
interface ComponentOptions {
  methods?: {
    [key: string]: (this: ComponentPublicInstance, ...args: any[]) => any
  }
}
```

## emits란?

컴포넌트에서 내보낼 커스텀 이벤트를 선언하는것이다.
emits를 이용해 부모 컴포넌트에 이벤트를 전달할 수 있다.

methods와 emits를 이용해 부모컴포넌트에 이벤트를 전달해보자

저번 v-model을 이용해 input값을 받는 프로젝트에 바로 적용해보면

```javascript
<script>
export default {
  emits: ["add-contact"],
  data() {
    return {
      enteredName: "",
      enteredTel: "",
      enteredEmail: "",
    };
  },
  methods: {
    submitData() {
      this.$emit(
        "add-contact",
        this.enteredName,
        this.enteredTel,
        this.enteredEmail
      );
    },
  },
};
</script>
```

먼저 풀어서 보자면 부모컴포넌트에 전달할 이벤트를 emits를 사용하여 “add-contact”를 선언한다.

그리고 methods를 사용하여 submitData라는 함수를 선언하고 emits에 선언해뒀던 “add-contact”를 $emit으로 불러온다.

$emit(‘전달할 이벤트 이름’,’~전달할 데이터~’…)로 사용한다.
submitData라는 함수가 실행될때, 프로젝트에선 enteredName, enteredTel, enteredEmail을 부모에게 전달해준다.

그리고 이벤트를 전달받는 부모 컴포넌트에서는
@add-contact로 정의해야 할 메서드를 가르킨다.
그리고 그 메서드의 이름을 addContact로 한다.
```javascript
<!-- App.vue 부모 컴포넌트 -->

<header><h1>My Friends</h1></header>
    <new-friend @add-contact="addContact"></new-friend>
```
```javascript
<script>
export default {
  methods: {
    addContact(name, phone, email) {
      const newFriendContact = {
        id: new Date().toISOString,
        name: name,
        phone: phone,
        email: email,
        isFavorite: false,
      };
      this.friends.push(newFriendContact);
    },
  },
};
</script>

```
(1) 버튼 클릭 이벤트 발생 $emit(‘add-contact) 실행
(2) 자식 -> 부모 ‘add-contact 이벤트 내보냄
(3) 부모에서 @add-contact로 이벤트 수신하고 addContact 함수 실행

### 정리
자식 컴포넌트에서 입력받은 데이터들을 v-model로 양방향 바인딩을 하고 emits를 통해 부모에게 전달할 함수 add-contact 를 선언한다. 선언된 함수는 methods를 사용해 sumbitData함수가 트리거 될때 실행됨에 따라 부모 컴포넌트에게 데이터를 전달한다.

부모 컴포넌트에서 add-contact 메서드 정의를 받고 메서드 이름을 addContact로 한다.

