<template>
  <div id="menu" :class="{on:is_on}" @click="menu_client()"><i></i></div>
  <div id="content" ref="content" @click="menu_close()">
    <router-view></router-view>
    <!--    <Background @background="set_background"></Background>-->
    <div id="message"></div>
   <div style="position: fixed;bottom: 0px;width: 100%;">
			<HR SIZE=1>
        <center>
				©2021-2023 
		               <a href="https://hhyblog.top" target="_blank" class="embed">
		               <img src="img/search.png" style="height: 13px;">我的博客 
		               </a>
		               All rights reserved
				<br>
				<font size="2">共</font>
        <span id="busuanzi_value_page_pv" size="2"><i class="fa fa-spinner fa-spin"></i></span>
				<font size="2">次访问&nbsp</font>
				<font id="box1" size="2"></font>
        </center>
				<script>
						 function timingTime(){
						 let start = '2021-5-20 00:00:00'
						 let startTime = new Date(start).getTime()
                                                 let currentTime = new Date().getTime()
                                                 let difference = currentTime - startTime
                                                 let m =  Math.floor(difference / (1000))
                                                 let mm = m % 60  // 秒
                                                 let f = Math.floor(m / 60)
                                                 let ff = f % 60 // 分钟
                                                 let s = Math.floor(f/ 60) // 小时
                                                 let ss = s % 24
                                                 let day = Math.floor(s  / 24 ) // 天数
                                                 return "已安全运行"+day + "天" + ss + "时" + ff + "分" + mm +'秒'
                                               }
                                               setInterval(()=>{
                                                 document.getElementById('box1').innerHTML = timingTime()
                                               },1000)
                                 </script>
			</div>
  </div>
</template>
<script>
import packageJson from '../package.json'
// import storage from "@/utils/storage";
// import axios from "axios";
import Bookmarks from "@/components/Bookmarks";
import Setting from "@/components/Setting";

export default {
  name: "Home",
  components: {Setting, Bookmarks},
  data() {
    return {
      version: packageJson.version,
      is_on: false,
      menu_selected: "bookmark",
      background: "",
    }
  },
  methods: {
    menu_client() {
      this.is_on = !this.is_on
    },
    menu_close() {
      this.is_on = false
    },
    menu_select(val) {
      this.menu_selected = val
    },
    set_background(data) {
      this.background = data;
    },
  },
  watch: {
    background() {
      try {
        this.$refs.content.style.background = this.background
      } catch (error) {
        console.log(error);
      }
    }
  },
  mounted() {
    this.$refs.content.style.background = this.background
  }
};
</script>

<style lang='less'>
@import "style/main";
</style>
