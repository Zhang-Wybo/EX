<template>
  <div id="app">
   <ComHeader></ComHeader>
   <router-view/>
   <ComFooter></ComFooter>
  </div>
</template>
<script>
//@代表引用src文件夹
import  ComHeader from './components/ComHeader';
import  ComFooter from '@/components/ComFooter';

export default {
  components: {
    ComHeader,
    ComFooter,
    
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
 
  margin-bottom: 1rem;
  
}

  a {
    font-weight: bold;
    color: black;

    &.router-link-exact-active {
      color: #ffffff;
    }
  }

</style>
