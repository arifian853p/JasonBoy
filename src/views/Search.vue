<template>
  <div>
    <div class="search-container">
      <div class="search">
        <input v-model="inp" type="text" />
        <div class="img">
          <img @click="search" src="../../public/Search.png" alt="" />
        </div>
      </div>
      <div style="display: flex">
        <div class="results">
          <div class="result" v-for="(item,index) in resultList" :key="index">
            <img :src="'http://localhost:8080/biyesheji/audio/read/'+item.img" alt="" />
            <div class="info">
              <p>{{item.name}}</p>
              <p><span>分类：</span>{{item.type}}</p>
            </div>
            <p class="author"><span>by：</span>江南</p>
            <p class="time"><span>时长：</span>20:12</p>
            <img class="play" @click="toPlay(item.id)" src="../../public/play.png" alt="" />
          </div>
        </div>
        <div class="rank-list">
          <div class="title">
            <img src="../../public/rank.png" alt="" />
            <p>每日热门</p>
          </div>
          <div class="lists">
            <div class="list">
              <img src="../../public/first.png" alt="" />
              <p>重生之我是UZI重生之我是UZI重生</p>
            </div>
            <div class="list">
              <img src="../../public/second.png" alt="" />
              <p>重生之我是UZI重生之我是UZI重生</p>
            </div>
            <div class="list">
              <img src="../../public/third.png" alt="" />
              <p>重生之我是UZI重生之我是UZI重生</p>
            </div>
            <div class="list">
              <img src="../../public/4.png" alt="" />
              <p>重生之我是UZI重生之我是UZI重生</p>
            </div>
            <div class="list">
              <img src="../../public/5.png" alt="" />
              <p>重生之我是UZI重生之我是UZI重生</p>
            </div>
            <div class="list">
              <img src="../../public/6.png" alt="" />
              <p>重生之我是UZI重生之我是UZI重生</p>
            </div>
            <div class="list">
              <img src="../../public/7.png" alt="" />
              <p>重生之我是UZI重生之我是UZI重生</p>
            </div>
            <div class="list">
              <img src="../../public/8.png" alt="" />
              <p>重生之我是UZI重生之我是UZI重生</p>
            </div>
            <div class="list">
              <img src="../../public/9.png" alt="" />
              <p>重生之我是UZI重生之我是UZI重生</p>
            </div>
          </div>
          <div class="title title2">
            <img src="../../public/rank.png" alt="" />
            <p>最多人搜</p>
          </div>
          <div class="lists">
            <div class="list">
              <img src="../../public/first.png" alt="" />
              <p>重生之我是UZI重生之我是UZI重生</p>
            </div>
            <div class="list">
              <img src="../../public/second.png" alt="" />
              <p>重生之我是UZI重生之我是UZI重生</p>
            </div>
            <div class="list">
              <img src="../../public/third.png" alt="" />
              <p>重生之我是UZI重生之我是UZI重生</p>
            </div>
            <div class="list">
              <img src="../../public/4.png" alt="" />
              <p>重生之我是UZI重生之我是UZI重生</p>
            </div>
            <div class="list">
              <img src="../../public/5.png" alt="" />
              <p>重生之我是UZI重生之我是UZI重生</p>
            </div>
            <div class="list">
              <img src="../../public/6.png" alt="" />
              <p>重生之我是UZI重生之我是UZI重生</p>
            </div>
            <div class="list">
              <img src="../../public/7.png" alt="" />
              <p>重生之我是UZI重生之我是UZI重生</p>
            </div>
            <div class="list">
              <img src="../../public/8.png" alt="" />
              <p>重生之我是UZI重生之我是UZI重生</p>
            </div>
            <div class="list">
              <img src="../../public/9.png" alt="" />
              <p>重生之我是UZI重生之我是UZI重生</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data(){
    return {
      resultList:[],
      inp:''
    }
  },
  methods:{
    toPlay(e){
      this.$router.push('/player?id='+e)
    },
    getList(){
      const url = "http://localhost:8080/biyesheji/audio/list";
      axios.get(url).then((res) => {
        for (let i = 0; i < res.data.length; i++) {
          if (i % 7 == 0) {
            this.resultList.push(res.data[i]);
          }
        }
        console.log(res.data);
      });
    },
    search(){
      axios.get('http://localhost:8080/biyesheji/audio/search/list/'+this.inp).then(res=>{
        this.resultList = res.data
      })
    }
  },
  watch:{
    inp(n,o){
      if (n=='') {
        this.getList()
      }
    }
  },
  mounted(){
    this.getList()
  }
};
</script>

<style scoped>
.search-container {
  width: 1180px;
  border: 1px solid black;
  margin: 0 auto;
}
.search {
  width: 100%;
  height: 160px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.search input {
  width: 320px;
  height: 44px;
  padding-left: 20px;
  border-radius: 6px 0 0 6px;
  border: 1px solid #ccc;
  box-shadow: inset -2px 2px 2px #ccc;
  outline: none;
}
.search .img {
  width: 44px;
  height: 44px;
  background-color: #eee;
  border: 1px solid #ccc;
  text-align: center;
  cursor: pointer;
}
.search img {
  width: 32px;
  height: 32px;
  margin-top: 6px;
}
.results {
  width: 900px;
  border: 1px solid black;
  padding: 20px;
}
.result {
  width: 860px;
  height: 100px;
  border: 1px solid #ccc;
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}
.result img {
  width: 100px;
  height: 100px;
}
.result .info {
  height: 100px;
  width: 200px;
  color: rgb(110, 109, 109);
  margin-left: 20px;
}
.result .info p:first-child {
  margin-top: 20px;
  font-size: 16px;
}
.result .info p:last-child {
  margin-top: 8px;
  font-size: 14px;
}
.result .author {
  margin-left: 150px;
  width: 160px;
  color: rgb(110, 109, 109);
}
.result .time {
  color: rgb(110, 109, 109);
  width: 100px;
}
.result .play {
  width: 60px;
  height: 60px;
  margin-left: 40px;
  cursor: pointer;
}
.rank-list {
  width: 280px;
  border: 1px solid black;
  padding: 0 20px;
}
.rank-list .title {
  width: 100%;
  height: 48px;
  display: flex;
  align-items: center;
  border-bottom: 1px solid #ccc;
}
.rank-list .title img {
  width: 24px;
  height: 24px;
  margin-right: 8px;
}
.rank-list .lists {
  margin-top: 20px;
}
.rank-list .list {
  height: 44px;
  display: flex;
  align-items: center;
  color: rgb(110, 109, 109);
}
.rank-list .list img {
  width: 32px;
  height: 32px;
}
.rank-list .list p {
  width: 200px;
  margin-left: 10px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  font-size: 14px;
}
.rank-list .title2 {
    margin-top: 10px;
}
</style>>
