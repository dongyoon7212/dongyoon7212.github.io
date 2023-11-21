---
layout: single
published: true
title: (Vue.js) slot, slot에 이름넣기
categories: 공부노트
tag: Vue.js
toc: true
toc_sticky: true
toc_label: 순간이동
sidebar:
    nav: "counts"
---

- - -
## slot이란?

Slot : 특정 컴포넌트에서 자신에게 등록된 자식 컴포넌트의 내용을 재정의 할 수 있는 디렉티브

slot은 컴포넌트의 재사용성을 높여주는 기능이다.

- - -
## slot 사용방법

```html
<-- UserInfo.vue -->

<template>
  <section>
     <header>
       <h3>{{ fullName }}</h3>
       <base-badge :type="role" :caption="role.toUpperCase()"></base-badge>
     </header>
     <p>{{ infoText }}</p>
  </section>
</template>
```
예를 들어 여기서 header 부분을 재사용 할 수 있게 slot으로 만들어보자

재사용할 컴포넌트를 새로 만든 뒤 재사용할 요소들을 넣는다.
```html
<-- BaseCard.vue -->

<template>
  <div>
    <slot></slot>
  </div>
</template>

<script>
export default {
  props: ["content"],
};
</script>

<style scoped>
div {
  margin: 2rem auto;
  max-width: 30rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 1rem;
}
</style>
```

위와 같이 template태그 안 header태그 역할을 대신할 div태그를 만들고 안에 slot태그를 넣는다.

그리고 header스타일 속성이던걸 그대로 가져와 div 스타일 속성으로 한다.

다음으로 UserInfo컴포넌트로 돌아와 slot으로 바꾼다.
```html
<-- UserInfo.vue -->

<template>
  <section>
    <base-card>
      <h3>{{ fullName }}</h3>
      <base-badge :type="role" :caption="role.toUpperCase()"></base-badge>
      <p>{{ infoText }}</p>
    </base-card>
  </section>
</template>
```
UserInfo에서 전역 컴포넌트로 등록 해뒀던 base-card로 불러와 태그를 씌운다.

이렇게 하면 header의 요소를 따로 재사용 가능한 컴포넌트로 만들어 사용할 수 있다.

- - -
## 만약 여러개의 slot을 중첩해서 쓴다면?

여러개의 slot을 중첩해서 사용한다면 slot에 이름을 부여하면 사용할 수 있다.

예를 들어 base-card태그 안 요소도 컨테이너로 감싼다고 생각하면
```html
<-- UserInfo.vue -->

<template>
  <section>
    <base-card>
      <h3>{{ fullName }}</h3>
      <base-badge :type="role" :caption="role.toUpperCase()"></base-badge>
      <p>{{ infoText }}</p>
    </base-card>
  </section>
</template>
```

다시 BaseCard로 돌아와 UserInfo컴포넌트의 구조와 같도록 만든다.
```html
<-- BaseCard.vue -->

<template>
  <div>
    <header>
        <slot name="header"></slot>
    </header>
    <slot></slot>
  </div>
</template>
```

여러개의 slot을 사용할 경우 이름을 지정해줘야 한다. 이때 두개 중 하나를 이름을 지정하면 다른 하나는 이름을 지정할 필요가 없다.

다시 UserInfo컴포넌트에서 적용시켜보자
```html
<-- UserInfo.vue -->

<template>
  <section>
    <base-card>
      <template v-slot:header>
        <h3>{{ fullName }}</h3>
        <base-badge :type="role" :caption="role.toUpperCase()"></base-badge>
      </template>
      <template v-slot:default>
        <p>{{ infoText }}</p>
      </template>
    </base-card>
  </section>
</template>
```
base-card 태그 안에 slot을 사용하기 위해선 template태그로 감싸준 뒤 v-slot:이름 옵션을 더해준다.

이때 default는 기본값이므로 렌더링 되지않고 컨테이너로 사용된다.

