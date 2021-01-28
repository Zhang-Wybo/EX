<template>
  <footer :style="{backgroundColor: curMenu.bgColor}">
    <div 
    v-for=" menu in menuList" 
    :key=" menu.path"  
    @click="switchMenu(menu)">
      <router-link :to="menu.path">{{menu.name}}</router-link>
    </div> 
    <!-- <router-link to="/music">音乐</router-link>
    <router-link to="/book">书籍</router-link>
    <router-link to="/chat">聊天</router-link> -->
    
  </footer>
</template>

<script>

import{mapState, mapMutations} from "vuex";
export default {
  computed: {
    ...mapState(["curMenu"])
  },
  data () {
    return {
      menuList:[
        {path:'/',name:'剧集',bgColor:'#ff0000'},
        {path:'/music',name:'音乐',bgColor:'#FF8C00'},
        {path:'/book',name:'书籍',bgColor:'#87CEFA'},
        {path:'/chat',name:'聊天',bgColor:'#FFD700'}

      ]
    };
  },
  methods: {
    ...mapMutations(["setCurMenu"]),
    switchMenu(menu){
      this.setCurMenu(menu);

    }
  }  
}
</script>
<style lang="scss" scoped>
footer{
  display: flex;
  justify-content: space-around;
  position: fixed;
  bottom: 0;
  width: 100%;
  height: 1rem;
  line-height: 1rem;
  text-align: center;
  background: cornflowerblue;
}
span{
  position: absolute;
  left: 0;
}

</style>
