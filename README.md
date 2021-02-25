# Tìm hiểu về scss

### Nested
```html
<div class="parent">
  <div class="parent__child">
    <p>Children</p>
  </div>
</div>

```

```scss
$bg-color-test: rgb(214, 84, 84);

.parent {
  background-color: $bg-color-test;
  &__child {
    color: aqua;
  }
}
```

> Công thức khai báo property cho các element HTML khi kết hợp giữa BEM và Sass

```scss
.block{
  
  &__element{

    &--modifier{

    }
  }
}
```

#### Nested Property

```scss
.text {
  font: {
    size: 1.5rem;
    family: 'arial';
    weight: bold;
  }
}

```

### 
 - Lấy giá trị các biến lưu trữ
- Áp dụng Selectors và tên thuộc tính css
- Cú pháp:

```scss
$bg-color-test: rgb(214, 84, 84);
$key: 'color';

.parent {
  background-color: $bg-color-test;
  h3 {
    font-size: 20px;
  }

  &:hover h3 {
    // Interpolation 
    #{$key}: blue;
  }
  &__child {
    color: aqua;

    .text {
      font: {
        size: 1.5rem;
        family: 'arial';
        weight: bold;
      }
    }
  } 
}
```

### Mixins trong Sass

**Mixins** là cách mà Sass dùng để dùng lại 1 đoạn code lặp đi lặp lại nhiều lần.

```scss
@mixin CSSlink {
  color: red;
  text-decoration:none;
}

.list{
  margin: 10px;
  
  &__link{
      @include CSSlink;
  }
}
```
> Sử dụng mixins cũng hoàn toàn có thể kết hợp với sử dụng biến. Trong ví dụ trên ta tiếp tục thay đổi 1 chút:

```scss
@mixin CSSlink($color, $status) {
  color: $color;
  text-decoration: $status;
}

.list{
  margin: 10px;
  
  &__link{
      @include CSSlink(red,none);
  }
```

### Functions trong Sass

Việc sử dụng **`Function`** trong Sass dùng để khai báo các giá trị của property với các công thức toán học (thường là chỉ sử dụng cho số đo như **width**, **margin**, **padding**,…)
```scss
@function TênFunction ($variable1, $variable2, ...) {

      @return Value;

}
```

Ví dụ:

```scss
@mixin CSSlink($color, $status) {
  color: $color;
  text-decoration: $status;
}

@function calMargin($a, $b){
  @return $a*$b;
}

.list{
  margin: calMargin(2,5)*1px;
  
  &__link{
      @include CSSlink(red,none);
  }
}
```

### Extends trong Sass

**Extends** trong Sass cũng tương tự như `mixins` nó có thể kế thừa một `placeholder`, `#id`, or `class`

```
%tênExtend {

    .....

}
```

Ta tiếp tục sử dụng Extend trong ví dụ trên:

```scss
%CSSlink{
color: red;
text-decoration: none;
}

.list{
  margin: calMargin(2,5)*1px;
  
  &__link{
      @extend %CSSlink;
  }
}


.parent2 {
  @extend .parent;
  // background-color: $bg-color-test;
  // h3 {
  //   font-size: 20px;
  // }

  // &:hover h3 {
  //   // Interpolation 
  //   #{$key}: blue;
  // }
  &__child2 {
    @extend .parent__child;
  } 
}
```

###  If Else trong scss
> Điều kiện logic là true/false có thể sử dụng toán tử logic ở dưới.

#### Toán tử logic
* `==` : so sánh bằng
* `!=` : so sánh khác
* `>` : so sánh lớn hơn
* `<` : so sánh nhỏ hơn
* `>=` : so sánh lớn hơn hoặc bằng
* `<=` : so sánh nhỏ hơn hoặc bằng

> Mixin my-font-type có tham số mạc định là $font với giá trị là '`base`', tùy tham số mà nó trả về thuộc tính `font-family` với font chữ tương ứng.
```scss
// SCSS
@mixin my-font-type($font: 'base') {
    @if ($font==bold) {
        font-family: 'Avenir-Demi';
    }
    @else if ($font==italic) {
        font-family: 'Avenir-LightItal';
    }
    @else {
        font-family: 'Avenir-Light';
    }
}

.title1 {
    @include my-font-type('bold');
    font-weight: bold;
}
.title2 {
    @include my-font-type('italic');
}
.title3 {
    @include my-font-type();
}
```

**Vòng lặp @for trong SCSS**

```scss
// SCSS
//Khai báo 4 biến lưu mã màu
$home: #F7E900;
$about: #FF5F09;
$news: #A0005E;
$links: #41004B;
//Tạo biến list (danh sách) với 4 phần tử trên
$pages: $home,
$about,
$news,
$links;

@for $i from 1 through length($pages) {
    body.page-#{$i} {
        background: nth($pages, $i);
    }
}


@each $item in $pages {
    body.section-#{ index($pages, $item)} {
        background: $item;
    }
}
```
>Hàm `length($pages)` trả về số phần tử chứa trong danh sách `$pages`, `nth($pages, $i)` lấy giá trị thứ `$i` trong danh sách $pages

### Map (key: value)

> Khai báo

```scss
  $sizes: (
    20: 20px,
    50: 50px,
    100: 100px
  );

  @each $key, $value in $sizes {
    body.section-#{$key} {
      with: $value;
    }
  }
```

## List method
```scss
/*
  append, nth, set-nth, length
*/
$list: 1px, 2px, 3px;

// tạo list mới, không ảnh hưởng đến list cũ
$newList: append($list, 4px);

$item: nth($list, 2); // giống slice

$new-item: set-nth($list, 1, 3px) 
```

## Map 

```scss
/**
  map-get, map-remove, map-merge, map-values
**/
```