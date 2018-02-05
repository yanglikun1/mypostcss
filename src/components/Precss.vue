<template>
  <div class="precss">
    <div class="menu">
     <span>我是嵌套！</span>
    </div>
    <div class="menu2">
     <span>我是判断语句</span>
    </div>
    <div class="div-1"></div>
    <div class="div-2"></div>
    <div class="div-3"></div>
    <div class="div-one"></div>
    <div class="div-two"></div>
    <div class="div-three"></div>
  </div>
</template>

<script>
export default {
  name: 'precss',
  data() {
    return {
      msg: 'Welcome to Your Vue.js App',
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/*变量*/
$color: blue;
$hei50: 50px;
$hei100: 100px;
$flagHei: 5;
$flagHei2: fivty;
/* 嵌套语法 */
.menu {
    width: 100%;
    span{
      color: red;
    }
    background: $color;
}
/*使用```&```符*/
.menu {
    span{
     &{
      border:1px solid red;
      }
    }
    &{
      border: 1px solid red;
    }
}
/*条件语句*/
.menu2 {
    span{
     &{
      border:1px solid red;
      }
    }
    &{
      border: 1px solid red;
    }
    background: yellow;
    @if $flagHei == 10 {
      height: $hei50;
    } @else {
      height: $hei100;
    }

    @if $flagHei2 == fivty {
      width: 200px;
    } @else {
      width: $hei100;
    }
}

/*循环@for @each*/
@for $i from 1 to 3 {
  .div-$i {
   background:red;
   height: calc($hei100 + $i*10px);
   width: calc($hei50 +  $i*5px);
  }
}
$ess: one, two, three;
@each $icon in ($ess) {
  .div-$(icon) {
      background:green;
      height: calc($hei100 + 10px);
     width: calc($hei50 + 5px);
  }
}
</style>
