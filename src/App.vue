<template>
  <div id="app">
   <PostcssCustomSelectors/>
  </div>
</template>

<script>
import Precss from './components/Precss';
import Mixins from './components/Mixins';
import PostcssCustomSelectors from './components/PostcssCustomSelector';

export default {
  name: 'App',
  components: {
    Precss, Mixins, PostcssCustomSelectors,
  },
};
</script>
<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
