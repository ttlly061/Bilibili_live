<template>
  <div
      @mouseover="hover = true"
      @mouseleave="hover = false"
      :class="{ active: hover }"
      ref="child2"
    > 
    <span v-if="hover">
      <div class="list-wrapper" style="overflow:auto">
        <el-scrollbar class="el-scrollbar__wrap">
        <dd v-for="(item,index) in list" :key="index">{{ item }}</dd>
        </el-scrollbar>
      </div>
      <div class="pannel">头号粉丝大航海 主播等你来上船</div>
    </span>
    <span v-else> 
      <dd>{{list[0]}}</dd>
      <dd>{{list[1]}}</dd>
      <dd>{{list[2]}}</dd> 
    </span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      hover: false,
      list: [1,2,3,4,5,6,7,8,9],
      loading: false,
      nowPage: 1,
      scrollHeight: 0,  
    }
  },
}
</script>

<style >
.list-wrapper {
  height: 100px;
}
.el-scrollbar {
  height: 100%;
}
.el-scrollbar__wrap {
  overflow: auto;
  overflow-x: hidden;
}
.pannel {
  position: relative;
  padding: 5px 8px;
  text-align: center;
  border: 1px solid rgb(226, 225, 225);
  border-radius: 3px;
  box-sizing: border-box;
  background: #fff;
  font-size: 15px;
}
</style>
