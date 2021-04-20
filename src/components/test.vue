<template>
  <div>
    <h2> vue 实现B站直播互动区 </h2>
    <div>
      <div class = "item">
        <button class="btn_anniu" @click="tabChange(child1)" :class="{ newStyle:isActive}">高能榜</button>
        <button class="btn_anniu" @click="tabChange(child2)" :class="{ newStyle:!isActive}">大航海</button>
      </div>
      <div :is="currentView"></div>
    </div>
    <div class = "chat_pannel">
      <el-scrollbar class="el-scrollbar__wrap">
      <dd v-for="(item,index) in list" :key="index">{{ item }}</dd>
      </el-scrollbar>
    </div> 
    <div ref="messages" class="messages"></div>
    <chat @send-message="sendMsg" @del-message="delMsg"/>
  </div>
</template>

<script>
// 导入子组件
import child1 from "@/components/child1";
import child2 from "@/components/child2";
import chat from "@/components/chat";
export default {
  data () {
    return {
      list: [],
      child1: "child1",
      child2: "child2",
      isActive: false,
      currentView: "child1", // 默认选中第一项
    };
  },
  methods: {
    tabChange(tabItem) {
      this.currentView = tabItem;
      this.isActive = !this.isActive;
    },
    sendMsg(childNodes, innerHTML) {
      console.log(childNodes); 
      this.list.push(innerHTML);
      console.log(this.list);
    },
    delMsg() {
      this.list = [];
    }
  },
  components: {
    child1,
    child2,
    chat,
  }
};
</script>

<style>
.btn_anniu {
  width: 50%;
  padding: 20px 0;
  font-size: 20px;
  font-weight: bold;
  border: 0 solid #fff;
  outline: none;
  background: #fff;
  vertical-align: middle;
  text-align: center;
}
.newStyle {
  font-weight: normal;
}
.chat_pannel {
  font-size: 15px;
  background: rgb(235, 215, 215); 
  text-align: center;
  flex-direction: column;
  color: #4889ca;
  height: 300px;
  min-width: 200px;
  min-height: 200px;
}
.messages {
  width: 100%;
  height: 100%;
  padding: 2px 5px;
  outline: none;
}
.el-scrollbar {
  height: 100%;
}
.el-scrollbar__wrap {
  overflow: auto;
  overflow-x: hidden;
}
</style>


        