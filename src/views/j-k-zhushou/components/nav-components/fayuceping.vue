<!--
 * @Descripttion: 
 * @version: 
 * @Author: sueRimn
 * @Date: 2021-05-17 09:41:20
 * @LastEditors: sueRimn
 * @LastEditTime: 2021-05-17 11:35:26
-->
<template>
  <div id="fayuceping">
    <van-nav-bar
      left-text="返回"
      left-arrow
      title="健康测评"
      @click-left="onClickLeft"
    ></van-nav-bar>
    <div class="biaoge">
      <div class="yihang">
        <div class="title">项目</div>
        <div class="fz">分值</div>
      </div>
      <div class="yihang-neirong">
        <div class="neirong">666</div>
        <div class="defen">aaa</div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "fayuceping",
  data(){
   return{
     data:[
       {
         neirong:'1.为了保证正确，做题总是做得很慢，做作业必须反复检查',
         fen:[1,2,3,4,5]
       },
       {
         neirong:'2.必须反复洗手或反复数数',
         fen:[1,2,3,4,5]
       },
        {
         neirong:'3.',
         fen:[1,2,3,4,5]
       },
        {
         neirong:'2.必须反复洗手或反复数数',
         fen:[1,2,3,4,5]
       }
     ]
   }
  },
  methods: {
    onClickLeft() {
      this.$router.go(-1);
    },
  },
};
</script>
<style scoped>
.biaoge {
  width: 100%;
}
.yihang {
  height: 20px;
  margin-top: 10px;
  display: flex;
  border: 1px solid #000;
}
.title {
  width: 70%;
  border-right: 1px solid #000;
  display: flex;
  justify-content: space-around;
  align-items: center;
}
.fz {
  width: 30%;
  display: flex;
  justify-content: space-around;
  align-content: center;
  align-items: center;
}
.yihang-neirong {
  height: 20px;
  border: 1px solid #000;
  border-top: 0px;
  display: flex;
}
.neirong {
  width: 70%;
  border-right: 1px solid #000;
  display: flex;
  border-left: 0px;
  align-items: center;
}
.defen {
  width: 30%;
  display: flex;
  align-items: center;
}
</style>