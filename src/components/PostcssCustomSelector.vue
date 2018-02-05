<template>
  <div class="postcsscustomselectors">
     <div class="icon">
       <span>111</span>
       <button>234</button>
       </div>
  <section><h1>你好</h1></section>
  </div>
</template>

<script>
export default {
  name: 'postcsscustomselectors',
  data() {
    return {
      msg: 'Welcome to Your Vue.js App',
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style >
/* @import './lib/style'; */
@import './lib/style' (min-width: 600px) and (orientation: landscape);
@custom-media --small-viewport (min-width: 600px) and (orientation: landscape);
/* @custom-media --phone (min-width: 700px) and (orientation: landscape); */

 .icon {
    width: 500px;
    height: 500px;
  }
@media (--small-viewport) {
  .icon {
    width: 100px;
    height: 100px;
    background: green;
  }
}

/* @media (--phone) {
  .icon {
    width: 100px;
    height: 100px;
    background: yellow;
  }
} */

</style>
