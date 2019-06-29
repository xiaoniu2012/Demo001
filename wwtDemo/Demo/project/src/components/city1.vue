<template>
  <div>
    <div id="top" @click="back()">
      <img src="../assets/img/back.png" alt>
      {{dizhi.name}}
      <p>切换城市</p>
    </div>
    <input type="text" v-model="kuang" placeholder="输入学校、商务楼、地址" id="sousuo">
    <button @click="find()" id="tijiao">提交</button>
    <p id="lishi">搜索历史</p>
    <p>以往的搜索历史</p>
    <p v-text="kuang" id="jilu" v-show="n">78</p>
    <ul>
      <li :key="i" v-for="(v,i) in xidi" id="infor" @click="jumpshop1(i)"> 
        <p id="inforp">{{v.name}}</p>
        <p id="inforp2">{{v.address}}</p>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  name: "city1",
  data() {
    return {
      dizhi: "",
      xidi: "",
      kuang: "",
      n: false,
     //  m: "0",
    };
  },
  created() {
    this.dizhi = this.$route.query;
    this.find();
  },
  methods: {
    find() {
      const api =
        "https://elm.cangdu.org/v1/pois?city_id=" +
        this.dizhi.id +
        "&keyword=" +
        this.kuang +
        "&type=search";
      this.$http({
        url: api,
        methods: "get",
        data: {
          //post的请求参数
        }
      }).then(res => {
        //请求返回的数据res    
        this.xidi = res.data; 
        console.log(res.data);
     //    if (this.xidi.length > 1) {
      });
    },
    back() {
      this.$router.back();
    },
    jumpshop1(i){
          this.$store.commit("getgeohash", this.xidi[i].geohash);
          console.log(this.xidi[i].geohash);
          console.log(i)
         this.$router.push({
              name:"shop1"
         })
    }
  }
};
</script>
<style scoped>
#jilu {
  width: 100%;
  height: 50px;
  color: black;
  font-weight: bold;
  text-align: center;
  line-height: 50px;
}
#inforp {
  font-weight: bold;
  font-size: 0.18rem;
  margin-top: 6px;
}
#inforp2 {
  margin-top: 6px;
  font-size: 0.1rem;
  overflow: hidden;
  color: grey;
}
#infor {
  height: 50px;
}
li {
  height: 30px;
  border: 1px solid black;
}
/* #clear{
     width: 100%;
     height: 50px;
     line-height: 50px;
     font-size: 0.25rem;
     border-top: 1px solid black;
} */
#lishi {
  width: 100%;
  height: 15px;
  font-size: 0.1rem;
  background-color: darkslategray;
  margin-top: 10px;
}
#top {
  width: 100%;
  height: 40px;
  background-color: blue;
  color: white;
  font-size: 0.3rem;
  text-align: center;
  line-height: 40px;
}
#top p {
  font-size: 0.15rem;
  float: right;
  margin-right: 10px;
}
#top img {
  width: 20px;
  height: 20px;
  float: left;
  margin-top: 10px;
  margin-left: 5px;
}
#sousuo {
  margin-top: 10px;
  width: 96%;
  margin-left: 2%;
  border: 1px solid grey;
  height: 50px;
  color: gray;
  font-size: 0.2rem;
}
#tijiao {
  margin-top: 10px;
  width: 96%;
  margin-left: 2%;
  border: 1px solid blue;
  background-color: blue;
  height: 50px;
  color: gray;
  font-size: 0.2rem;
  border-radius: 5px;
}
</style>
