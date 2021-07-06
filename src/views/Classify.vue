<template>
  <div class="classify-container">
    <div class="top">
      <div class="option" @click="pingshu1">评书</div>
      <div class="option" @click="xiangsheng1">相声</div>
      <div class="option" @click="xiaopin1">小品</div>
      <div class="option" @click="shici1">诗词</div>
      <div class="option" @click="sanwen1">散文</div>
      <div class="option" @click="yousheng1">有声小说</div>
      <div class="option" @click="lishi1">历史小说</div>
      <div class="option" @click="storge1">儿童故事</div>
      <div class="option" @click="other">其他</div>
      <div class="option" @click="all">全部</div>
    </div>
    <div class="main">
      <div class="title">全部作品</div>
      <div class="items">
        <div
          class="item"
          v-for="(i, j) in showingList"
          @click="toPlay(i.id)"
          :key="j"
        >
          <img :src="'http://localhost:8080/biyesheji/audio/read/'+i.img" alt="" />
          <p>{{ i.name }}</p>
          <p class="brief">{{ i.info }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      showingList: [],
    };
  },
  methods: {
    getList() {
      axios.get("http://localhost:8080/biyesheji/audio/list").then((res) => {
        console.log(res);
        this.showingList = res.data
      });
    },
    classifyList(data){
      axios.get('http://localhost:8080/biyesheji/audio/classify/list/'+data).then(res=>{
        this.showingList = res.data
      })
    },
    pingshu1() {
      this.classifyList('评书')
    },
    xiangsheng1() {
      this.classifyList('相声')
    },
    xiaopin1() {
      this.classifyList('小品')
    },
    shici1(){
      this.classifyList('诗词')
    },
    sanwen1(){
      this.classifyList('散文')
    },
    yousheng1(){
      this.classifyList('有声小说')
    },
    lishi1(){
      this.classifyList('历史小说')
    },
    other() {
      this.classifyList('其他')
    },
    storge1() {
      this.classifyList('儿童故事')
    },
    toPlay(e) {
      this.$router.push("/player?id=" + e);
    },
    all(){
      this.getList()
    }
  },
  mounted() {
    localStorage.setItem("storage", JSON.stringify(this.storge));
    this.getList();
  },
};
</script>

<style lang="less" scoped>
.classify-container {
  width: 1180px;
  margin: 0 auto;
}
.top {
  height: 140px;
  background-color: rgb(238, 238, 238);
  box-shadow: 2px 2px 2px #ccc;
  display: flex;
  flex-wrap: wrap;
  padding-bottom: 20px;
  .option {
    margin-top: 20px;
    width: 120px;
    background-color: rgb(219, 216, 216);
    height: 32px;
    border-radius: 16px;
    text-align: center;
    line-height: 32px;
    margin-left: 50px;
    cursor: pointer;
  }
}
.main {
  margin-top: 10px;
  background-color: rgb(238, 238, 238);
  box-shadow: 2px 2px 2px #ccc;
  padding: 0 20px;
  padding-bottom: 20px;
  .title {
    height: 44px;
    font-size: 20px;
    display: flex;
    align-items: center;
    border-bottom: 1px solid #000;
  }
  .items {
    display: flex;
    flex-wrap: wrap;
    margin-top: 20px;
    .item {
      width: 166px;
      height: 240px;
      margin-left: 20px;
      cursor: pointer;
      img {
        width: 100%;
        height: 180px;
        border-radius: 6px;
      }
      .brief {
        color: rgb(160, 160, 160);
        margin-top: 6px;
        font-size: 13px;
      }
    }
  }
}
</style>
