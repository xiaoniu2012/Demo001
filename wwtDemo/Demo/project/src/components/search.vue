<template>
  <div id="wrap">
    <div id="top">
        <img src="../assets/img/back.png" @click="back()">
      <p>搜索</p>
    </div>
    <div id="case">
      <input v-model="keyword" type="text" placeholder="请输入商家或美食名称">
      <p @click="find()">提交</p>
    </div>
    <ul>
      <li :key="i" v-for="(v,i) in food" id="serchimg">
        <img :src="'https://elm.cangdu.org/img/'+ v.image_path" alt="">
        <p>{{v.name}}</p>
        <p>{{v.distance}}</p>
        
      </li>
    </ul>

    <footer>
      <div>
        <router-link to="/takeout">
          <img src="../assets/img/SSS.png" alt>
          <br>
          <span>外卖</span>
        </router-link>
      </div>
      <div>
        <router-link to="/search">
          <img src="../assets/img/zhinanzhen1.png" alt>
          <br>
          <span>搜索</span>
        </router-link>
      </div>
      <div>
        <router-link to="/bos">
          <img src="../assets/img/dingdan1.png" alt>
          <br>
          <span>订单</span>
        </router-link>
      </div>
      <div>
        <router-link to="/my">
          <img src="../assets/img/touxiang2.png" alt>
          <br>
          <span>我的</span>
        </router-link>
      </div>
    </footer>
  </div>
</template>
<script>
export default {
  name: "search",
  data() {
    return {
      jingdu: "",
      food: [],
      keyword: ""
    };
  },
  created() {
    this.jingdu = this.$store.state.jingdu;
    console.log( this.$store.state.jingdu);
    this.find();
  },
  methods: {
    back(){
      this.$router.back();
    },
    find() {
      const api =
        "https://elm.cangdu.org/v4/restaurants?geohash="+this.jingdu+"&keyword="+this.keyword;
      this.$http({
        url: api,
        methods: "get",
        data: {
          //post的请求参数
        }
      }).then(res => {
        //请求返回的数据res
        this.food = res.data;
        console.log(this.food);
        if (this.food.length) {
          this.food.push({ name: "抱歉，无搜索结果" });
        }
      });
    }
  }
};
</script>
<style scoped>
#wrap {
  width: 3.75rem;
  position: relative;
  height: 100vh;
  background-color: rgb(245, 245, 245)
}
#top {
  width: 100%;
  height: 50px;
  background-color: rgb(49, 144, 232);
  position: fixed;
  z-index: 2;
}
#top img {
  height: 20px;
  position: absolute;
  left: 5%;
  top: 50%;
  transform: translate(-50%, -50%);
}
#top p {
  font-size: 0.15rem;
  color: white;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
#case {
  width: 100%;
  padding-top: 60px;
  height: 50px;
  background-color: white;
}
#case input {
  width: 2.75rem;
  height: 35px;
  background-color: rgb(242, 242, 242);
  border: 0.01rem solid rgb(242, 242, 242);
  font-size: 0.15rem;
  position: absolute;
  left: 8px;
  top: 62px;
}
#case p {
  width: 0.7rem;
  height: 38px;
  background-color: rgb(49, 144, 232);
  color: white;
  text-align: center;
  line-height: 38px;
  font-size: 0.15rem;
  position: absolute;
  left: 2.95rem;
  top: 61px;
}
footer {
  width: 3.75rem;
  height: 0.65rem;
  background-color: white;
  position: fixed;
  bottom: 0;
  display: flex;
  justify-content: space-around;
  font-size: 0.12rem;
}
footer div img {
  width: 0.25rem;
}
footer div {
  margin-top: 0.15rem;
}
#serchimg{
  width: 3.75rem;
  height: 0.75rem;
  /* border: 1px solid red; */
  position: relative;
}
#serchimg img:nth-child(1){
  position: absolute;
  left: 0.1rem;
  width: 0.45rem;
}
#serchimg p:nth-child(2){
  font-size: 0.2rem;
  /* width: 0.45rem; */
  position: absolute;
  left: 0.75rem;
}
#serchimg p:nth-child(3){
  font-size: 0.2rem;
  /* width: 0.45rem; */
  position: absolute;
  left: 0.7rem;
  top: 0.35rem;
}
</style>