<template>
  <div>
    <div class="header">
      <van-nav-bar title="基础信息" class="nav">
        <template #left>
          <van-icon
            name="arrow-left"
            size="20"
            class="arrow-left"
            @click="fh"
          />
        </template>

        <template #right>
          <van-icon name="ellipsis" size="20" class="right" />
        </template>
      </van-nav-bar>
    </div>
    <van-cell-group class="group">
      <ul class="step-container">
        <li class="step-past">
          身份信息
          <span class="arrow arrow-past">
            <span class="arrow-pre"></span>
            <span class="arrow-next"></span>
          </span>
        </li>
        <li class="step-current">
          基础信息
          <span class="arrow arrow-current">
            <span class="arrow-pre"></span>
            <span class="arrow-next"></span>
          </span>
        </li>
        <li class="step-next" style="background-color: #4461a5">归属门诊</li>
      </ul>
    </van-cell-group>

    <div class="header_search">
      <div class="header_addess">
        <van-icon name="location-o" class="dz" size="12" />
        <span>{{ this.dizhi || dizhi2 }}</span>
      </div>

      <van-search placeholder="请输入搜索关键词" class="search" />
    </div>

    <div style="position: relative; top: 40px">
      <div
        v-for="(item, i) in yuyue"
        @click="insurance(i)"
        :key="i"
        style="
          display: block;
          padding: 10px 10px;
          border-bottom: 1px solid #aaa;
          color: black;
        "
      >
        <p style="margin-bottom: 8px; font-weight: 500">{{ item.hcaddress }}</p>
        <div
          style="
            margin-bottom: 8px;
            display: flex;
            justify-content: space-between;
          "
        >
          <span style="color: #aaa; font-size: 12px">{{ item.hcinfor }}</span
          ><span>{{ item.vaccincount }}km</span>
        </div>
        <p style="margin-bottom: 15px">{{ item.hctime }}</p>
        <div style="display: flex; justify-content: space-between">
          <span style="color: #fbc"
            >剩余源号：<span>{{ item.vaccincoutnow }}</span></span
          ><button
            style="
              font-size: 12px;
              padding: 5px 15px;
              border-radius: 25px;
              border: 0;
            "
            @click.stop="xinxi"
          >
            选择门诊
          </button>
        </div>
      </div>
    </div>

    <div class="btn">
      <van-button type="default" class="btn1" @click="shangbu"
        >上一步</van-button
      >
      <van-button type="default" class="btn2" @click="xiabu1"
        >下一步</van-button
      >
    </div>
  </div>
</template>
<script>
import { yiyuanaccess } from "../../../../../components/axiosAPI";
import { mapState } from "vuex";
export default {
  data() {
    return {
      dizhi2: localStorage.getItem("dizhi2"),
      loading: false,
      value1: 0,
      value2: "a",
      option1: [{ text: this.dizhi, value: 0 }],
      yuyue: [],
    };
  },
  methods: {
     xinxi() {
      this.$router.push("/menzhen");
    },
    loadmore() {
      this.loading = true;
    },
    xiabu1() {
      this.$router.push("/yuyue");
    },
    fh() {
      this.$router.go(-1);
    },
    shangbu() {
      this.$router.go(-1);
    },
    insurance(id) {
      this.$router.push({
        path: `/addessxq/${id}`,
      });
    },
  },
  mounted() {
    this.loadmore();
    yiyuanaccess(localStorage.getItem("dizhi2")).then((res) => {
      this.yuyue = res.data.result;
      let yuyuexq = JSON.stringify(this.yuyue);
      sessionStorage.setItem("yuyuexq", yuyuexq);
    });
  },
  computed: {
    ...mapState(["dizhi"]),
  },
};
</script>

<style>
.dz {
  margin-left: -12px;
}

.header_addess {
  width: 20%;
  position: absolute;
  top: 16px;
  left: 21px;
  font-size: 15px;
}
.btn {
  text-align: center;
  margin-top: 1.5rem;
}
.btn .btn1 {
  width: 150px;
  height: 40px;
  border-radius: 5px;
  background-image: linear-gradient(#cae8ff, #7dc5ff);
  margin-right: 20px;
}
.btn .btn2 {
  width: 150px;
  height: 40px;
  border-radius: 5px;
  background-color: #45abc2;
  background-image: linear-gradient(#7dc5ff, #5c9bca);
  color: white;
}
.btn2 {
  margin-left: 40px;
}
.cell {
  font-size: 14px;
}
/* .group{
  font-weight: bold; 
   text-align: left;
} */
button {
  margin-top: 30px;
}
.step-conainer {
  margin: 0;
  padding: 0;
  width: 100%;
}
/* .header {
  /* border-bottom: 2px solid #eee; */
.step-container li {
  display: inline-block;
  position: relative;
  margin: 0;
  padding: 0;
  width: 33%;
  height: 30px;
  line-height: 30px;
  font-size: 14px;
  text-align: center;
  background-color: #ccc;
  color: #ffffff;
  margin-top: 20px;
}
.step-container li.step-past {
  background-color: #9cddf5;
  width: 34%;
}
.step-container li.step-current {
  background-color: #00a2ca;
}

.arrow {
  position: absolute;
  right: -7.5px;
  height: 30px;
  background-color: #ffffff;
  z-index: 2;
}
.arrow span {
  display: inline-block;
  border-left: 15px solid transparent;
  border-top: 15px solid transparent;
  border-bottom: 15px solid transparent;
}
/* .arrow-next { */
/* margin-left: -15px; */
/* } */
.arrow-past .arrow-pre {
  border-left: 15px solid #9cddf5;
}
.arrow-past .arrow-next {
  border-top: 15px solid #00a2ca;
  border-bottom: 15px solid #00a2ca;
}
.arrow-current .arrow-pre {
  border-left: 15px solid #00a2ca;
}
.arrow-current .arrow-next {
  border-top: 15px solid #4461a5;
  border-bottom: 15px solid #4461a5;
}
.arrow-current .step-next {
  background-color: #335daf;
}

.household {
  border-top: 10px solid #eee;
  border-bottom: 10px solid #eee;
}
.present {
  border-bottom: 10px solid #eee;
}
.company {
  border-bottom: 10px solid #eee;
}
.default {
  margin-top: 20px;
  font-size: 14px;
  margin-left: 20px;
  text-align: center;
  color: #8fdbfb;
}
.default span {
  color: #335daf;
}
.header_search {
  width: 100%;
  position: relative;
  border-top: 10px solid #eee;
  margin-top: 10px;
}

.dingwei .van-dropdown-menu__bar {
  margin-left: 0;
  position: absolute;
  top: 8px;
  height: 30px;
  width: 30%;
  box-shadow: none;
}
.search {
  width: 80%;
  position: absolute;
  right: 0;
  top: 0px;
}
</style>