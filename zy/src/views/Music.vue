<template>
  <div>
    <aplayer :audio="audio" :lrcType="3" />
    <ul>
        <li class="music-item">
            <span class="num">编号</span>
            <span class="name">歌曲名</span>
            <span class="artist">歌手名</span>
        </li>
        <li v-for="(item,index) in musicList" :key="item.id" class="music-item" @click="getSong(item.id)">
            <span class="num">{{index + 1}}</span>
            <span class="name">{{item.name}}</span>
            <span class="artist">{{item.ar[0].name}}</span>
        </li>
    </ul>
  </div>
</template>


<script>
import Vue from "vue";
import APlayer from "@moefe/vue-aplayer";

Vue.use(APlayer, {
  defaultCover: "https://github.com/u3u.png",
  productionTip: true
});
export default {
  created() {
    this.getData();
  },
  data () {
    return {
        audio: {
        name: '',
        artist: '',
        url: '',
        cover: '', // prettier-ignore
        // name: '东西（Cover：林俊呈）',
        // artist: '纳豆',
        // url: 'https://cdn.moefe.org/music/mp3/thing.mp3',
        // cover: 'https://p1.music.126.net/5zs7IvmLv7KahY3BFzUmrg==/109951163635241613.jpg?param=300y300', // prettier-ignore
      },
      musicList:[]
    }
  },

  methods: {
    getData() {
      this.axios
      .get("https://bird.ioliu.cn/netease/playlist?id=5446685214")
      .then((res) => {
          this.musicList = res.data.playlist.tracks;
          this.getSong(this.musicList[0].id)
        //   this.musicList = res.data.playlist.tracks.map((item)=>{
        //       return{
        //           name:item.name,
        //           id: item.id,
        //           artist:item.ar[0].name,
        //       }
        //   })
          console.log(res)
      });
    },
    getSong(id){
        this.axios
        .get("https://bird.ioliu.cn/netease/song?id=" + id)
        .then((res)=>{
            console.log(res);
            this.audio = {
                name: res.data.data.name,
                artist: res.data.data.ar[0].name,
                url: res.data.data.mp3.url,
                cover: res.data.data.al.picUrl
            };
        })
    }
  }
};
</script>



<style lang="scss" scoped>
.music-item{
    display: flex;
    .name{
        flex: 5;

    }
    .num{
        flex: 3;

    }
    .artist{
        flex: 4;

    }
}
</style>