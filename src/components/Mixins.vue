<template>
  <div class="mixins">
     <div class="icon">111</div>
     <div class="sen">555</div>
     <div class="logo">555</div>
  </div>
</template>

<script>
export default {
  name: 'mixins',
  data() {
    return {
      msg: 'Welcome to Your Vue.js App',
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style >

@define-mixin icon $color: blue {
     .icon {
       color: $color;
       width: 100px;
       height: 100px;

     }
    .icon:hover {
         color: white;
         background: $color;
     }
}

@mixin icon rgb(255, 0, 0);

/* @property size height width  {
  width: $height;
  height: $width;
}
.sen {
  +size: 100px 100px;
  background: yellow;
} */

@define-mixin icons $name {
    & {
        content: "123";
        padding-left: -16px;
        background: url(../assets/$(name).png) no-repeat;
        background-size: 100%;
    }
}

.logo {
    @mixin icons logo;
    width: 100px;
    height: 100px;
}

</style>
