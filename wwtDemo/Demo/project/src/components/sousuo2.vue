<template>
  <div>
    <div id="header">
      <span>{{name}}</span>
    </div>
    <div id="xinxi">
      <input id="shuru" v-model="keyword" placeholder="输入学校、商务楼、地址" type="text">
      <button @click="search()" id="tijiao">提交</button>
    </div>
    <ul>
      <li :key="i" v-for="(v,i) in food">
        <h3>{{v.name}}</h3>
        <p style="color:gray">{{v.address}}</p>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  name: "qiehuan",
  data() {
    return {
      name: "",
      id: "",
      keyword: "",
      food: ""
    };
  },
  created() {
    this.Add();
  },
  methods: {
    Add() {
    //   this.name = this.$route.query.cityName;
      this.id = this.$route.query;
    },
    search() {
      if (this.keyword == "") {
        return;
      } else {
        const api =
          "https://elm.cangdu.org/v1/pois?city_id=" +
          this.id +
          "&keyword=" +
          this.keyword +
          "&type=search";
        this.$http({
          url: api,
          method: "get"
        }).then(res => {
          this.food = res.data;
          // console.log(this.food);
        //   if (this.food.length == 0) {
        //     this.food.push({ name: "抱歉，无搜索结果" });
        //   }
        });
      }
    }
  }
};
</script>
<style scoped>
#header {
  height: 0.45rem;
  background-color: rgb(48, 144, 232);
  font-size: 0.16rem;
  color: white;
  line-height: 0.45rem;
  display: flex;
  justify-content: space-between;
  padding: 0 0.1rem 0 0.1rem;
}
#xinxi {
  text-align: center;
  margin-top: 0.1rem;
}
#shuru {
  width: 95%;
  height: 0.4rem;
}
#tijiao {
  background-color: rgb(48, 144, 232);
  width: 95%;
  height: 0.4rem;
  margin-top: 0.1rem;
}
ul {
  margin-top: 0.2rem;
}
ul li {
  padding: 0.2rem;
  background-color: white;
  border-bottom: 1px solid gray;
}
ul li p {
  margin-top: 0.2rem;
}
</style>