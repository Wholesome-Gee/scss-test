# Part5. SCSS

## ch.01 개요

## ch.02 프로젝트 생성

- SCSS 문법 예제

  ```html
  <!-- html -->
  <div class="container">
    <h1>HELLO SCSS!</h1>
  </div>
  ```

  ```scss
  // scss
  $color = royalblue; // color 변수 생성

  // scss의 중첩 개념 =
  .container {
    h1 {
      color: $color;
    }
  }
  ```

  <br/>

## ch03. 주석

- `/\*\*/`
- `//` ➡️ SCSS에서 CSS로 컴파일 할 땐 주석처리 된 줄이 사라진다.
  <br/>

## ch04. 중첩

- html
  ```html
  <div class="container">
    <ul/>
      <li>
        <div class="name">JIYONG</div>
        <div class="age">30</div>
      </li>
    </ul>
  </div>
  ```
- scss
  ```scss
  .container {
    ul {
      li {
        .name {
        }
        .age {
        }
      }
    }
  }
  ```
  <br/>

## ch05. 상위(부모)선택자 참조

- & 기호 사용

  ```scss
  // &는 상위선택자, 즉, .btn을 의미함.
  .btn {
    position: absolute;
    &.active {
      color: red;
    }
  }

  // &는 상위선택자, 즉 .li를 의미함
  .list {
    li {
      &:last-child {
        margin-right: 0;
    }
  }

  // &는 상위선택자, 즉 .fs를 의미함
  .fs {
    &-small { font-size: 12px;}  // .fs-small { font-size: 12px; }
    &-medium { font-size: 14px;} // .fs-medium { font-size: 14px; }
    &-large { font-size: 16px;}  // .fs-large { font-size: 16px; }
  }
  ```

<br/>

## ch06. 중첩된 속성

- 중첩되는 속성 이름을 간편화 할 수 있다.(name space 속성 간편화)
- css
  ```css
  .box {
    font-weight: bold;
    font-size: 10px;
    font-family: sans-serif;
    margin-top: 10px;
    margin-left: 20px;
    padding-top: 10px;
    padding-bottom: 40px;
    padding-left: 20px;
    padding-right: 30px;
  }
  ```
- scss
  ```scss
  .box {
    font: {
      weight: bold;
      size: 10px;
      family: sans-serif;
    }；
    margin: {
      top: 10px;
      left: 20px;
    }；
    padding: {
      top: 10px;
      bottom: 40px;
      left: 20px;
      right: 30px;
    }；
  }
  ```
  <br/>

## ch07. 변수

- $ 기호로 변수를 지정할 수 있다.
- 선언된 블록 내에서 유효범위를 갖는다.
- 하위 선택자에 있는 변수가 우선순위를 갖는다.

  ```scss
  .container {
    $size: 200px; // 지역 변수 지정
    position: fixed;
    top: $size; // 변수 사용
    .item {
      $size: 100px; // size 변수 값이 200px → 100px로 변경
      width: $size;
      height: $size;
      transform: translateX($size);
    }
    left: $size; // 100px → .item 내부에 있는 size변수가 전역 size변수의 값을 바꿔 놓음
  }
  ```

  <br/>

## ch08. 산술 연산

- 산술 연산자 사용 가능하다.
- 같은 단위의 값들만 연산이 가능하며, calc 함수를 사용했을 시만 다른 단위끼리의 연산이 가능하다.

```scss
// 나누기는 소괄호로 묶던가, 변수와 같이 사용하던가, 다른 연산자와 함께 사용하던가 해야한다.
.div {
  width: 20px + 20px; // 40px
  height: 40px - 10px; // 30px
  font-size: 10px * 2; // 20px
  margin: (30px / 2); // 15px
  // $size: 30px;
  // margin: $size / 2;
  // margin: (10 + 20) / 2;
  padding: 20px % 7; // 6px
}

// '/'기호는 다른 용도로 쓰인다.
span {
  font-size: 10px;
  line-height: 10px;
  font-family; serif;
  font: 10px / 10px serif;
}

.div {
  width: calc(100% - 200px);
}
```

  <br/>

## ch09. 재활용(Mixins)

- `@mixin` 재활용 선언 / `@include` 재활용 사용

  ```scss
  // 재활용 선언
  @mixin center {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .container {
    @include center; // 재활용 사용
    .item {
      @include center; // 재활용 사용
    }
  }
  ```

- 재활용의 인수 사용

  ```scss
  // 재활용 인수 선언
  @mixin box($size: 100px, $color: tomato) {
    // size의 기본값은 100px
    // color의 기본값은 tomato
    width: $size;
    height: $size;
    background-color: $tomato;
  }

  .container {
    @include box(200px, red); // 재활용 인수 사용
    .item {
      @include box; // 재활용 인수가 없다면 기본값인 size: 100px이 적용됨
    }
    .title {
      @include box($color: green); // 키워드 인수
    }
  }
  ```

  <br/>

## ch10. 반복문

- `@for $i from 1 through 10`으로 10번 반복문을 작성할 수 있다.

```scss
// i가 1번부터 시작해서 10까지 반복
// #{}는 js의 ${}와 같은 역할
@for $i from 1 through 10 {
  .box:nth-child(#{$i}) {
    width: 100px * $i;
  }
}
```
