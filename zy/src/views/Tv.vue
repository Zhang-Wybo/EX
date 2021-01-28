<template>
  <div>
    <ul class="tv-list">
      <li class="tv-item" v-for="item in tvList" :key="item.id"
      @click="getDetail(item.id)">
        <div class="img">
          <!-- <img :src="item.cover.url" alt /> -->
          <!-- 如果图片显示不出来用下面代码 -->
          <img :src=" 'https://images.weserv.nl/?url='+ item.cover.url" alt />
        </div>
        <div class="content">
          <h3>{{item.title}}</h3>
          <p>{{item.info}}</p>
        </div>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  data() {
    return {
      tvList: [],
      start: 0,
      isFinish: true
    };
  },
  created() {
    this.getData();
  },
  mounted() {
    this.listenScroll();
  },
  methods: {
    //跨域问题：当你网页所在地址与你接口地址（包括协议，域名，端口号）任何一个不一样，都会引发跨域
    //解决：jsonp,CORS(后端),第三方服务器代理

    //获取电视剧列表的数据
    getData() {
      if (this.isFinish) {
        this.isFinish = false;
        // let baseUrl = "http://bird.ioliu.cn/v2?url=";
        // let tvUrl = `https://m.douban.com/rexxar/api/v2/subject_collection/tv_domestic/items?os=ios&for_mobile=1&start=${this.start}&count=10`;
        // this.axios
        //   .get(baseUrl + tvUrl)
        this.axios
          .get("https://bird.ioliu.cn/v2?url=https://m.douban.com/rexxar/api/v2/subject_collection/tv_domestic/items",
          {
            params: {
                start: this.start,
                count: 10,
              },
            }
          )
          .then((res)  => {
            console.log(res);
            // this.tvList = this.tvList.concat(res.data.subject_collection_items);
            this.tvList = [
              ...this.tvList,
              ...res.data.subject_collection_items,
            ];
            this.isFinish = true;
            //  console.log(this.tvList);
            //  console.log(res.data)
          })
          .catch((err)=> console.log(err));
      }
    },
    //处理数据懒加载
    listenScroll() {
      //获取html元素
      let htmlDom = document.documentElement;
      //获取窗口高度
      let deviceHeigth = htmlDom.clientHeight;
      // console.log(deviceHeigth)
      let fullHeight = 0;
      let scrollTop = 0;
      window.onscroll = () => {
        //页面总高度
        fullHeight = htmlDom.offsetHeight;
        //滚动条距离顶部的距离
        scrollTop = htmlDom.scrollTop;
        if (scrollTop + deviceHeigth > fullHeight - 20) {
          if(this.start < 40){
            this.start += 10;
            this.getData();
          }
          // this.start += 10;
          // if (this.start < 50) {
            
          //   this.getData();
          // }
          console.log("滚动到底部啦");
        }
        // console.log(htmlDom.offsetHeight);
        // console.log(htmlDom.scrollTop);
      };
    },
    //跳转电视剧详情页
    getDetail(id) {
      this.$router.push('/tvdetails/'+ id)

    }
  }
};
</script>
<style lang="scss" scoped>
.tv-list {
  .tv-item {
    display: flex;
    padding: 10px;
    border-bottom: 1px solid #cccccc;
    .img {
      flex: 3;
      img {
        width: 100%;
      }
    }
    .content {
      flex: 5;
      padding: 10px;
      h3 {
        font-weight: bolder;
        margin-bottom: 20px;
      }
    }
  }
}
</style>
