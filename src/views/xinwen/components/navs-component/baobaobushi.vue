<!--
 * @Descripttion: 
 * @version: 
 * @Author: sueRimn
 * @Date: 2021-05-17 14:48:26
 * @LastEditors: sueRimn
 * @LastEditTime: 2021-05-17 14:48:36
-->
<template>
  <div id="baobaobushi">
    <div style="display:fixed;width:100%;height:50px;background-color:#fff;z-index:1;text-align:center;">
          <div @click="back()" style="width:30px;height:30px;float:left;padding:10px;"><img style="width:100%;height:100%;" src="../../../../assets/xwen/back.svg" alt=""></div>
          <div style="font-size:20px;line-height:50px;">宝宝辅食食谱</div>
    </div>
    <div>
      <van-tabs>
          <van-tab v-for="(item,index) in sp" :key="index" :title="item.id+'月龄'">
              <div style="margin:10px 10px;">
                <p style="font-size:16px;font-weight:550;">{{item.id}}月龄宝宝辅食营养指导</p>
                <div style="margin-top:10px;font-size:16px;color:black;line-height:150%;" v-html="item.nr"></div>
              </div>
          </van-tab>
      </van-tabs>
    </div>
  </div>
</template>
<script>
import { Tab, Tabs } from 'vant';
export default {
  data(){
    return {
      sp:[]
    }
  },
  methods:{
     back(){
          this.$router.go(-1);
        },
        loadshipu(){
          this.axios.get('/shipu').then(res=>{
            this.sp=res.data.result;
          })
        }
  },
  mounted(){
    this.loadshipu();
  }
}
</script>
<style scoped>

</style>