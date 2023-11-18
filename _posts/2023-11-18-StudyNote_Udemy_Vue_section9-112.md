---
layout: single
title: (Vue.js) 전역 스타일, 지역 스타일
categories: 공부노트
tag: Vue.js
toc: true
toc_sticky: true
toc_label: 순간이동
sidebar:
    nav: "counts"
---

- - -

## 전역 스타일과 지역 스타일 적용법

#### 전역 스타일
- `<style></style>`로 사용하며 앱 전체에 스타일을 적용시킴

#### 지역 스타일
- `<style scoped></style>` scoped 옵션 추가, 해당 컴포넌트에서만 스타일을 적용시킴

- - -
#### 예제

전역 스타일로 사용할 때
```javascript
<style>
html {
  font-family: sans-serif;
}

body {
  margin: 0;
}
</style>
```

`<style></style>` 태그로만 사용하면 앱 전체에 해당 스타일 모두 적용

지역 스타일로 사용할 때
```javascript
<style scoped>
section {
  margin: 2rem auto;
  max-width: 30rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 1rem;
}

section header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
```

`<style scoped></style>` 로 scoped 옵션을 추가하면 해당 컴포넌트에서만 스타일 적용
