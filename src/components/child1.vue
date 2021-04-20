<template>
  <div
      @mouseover="hover = true"
      @mouseleave="hover = false"
      :class="{ active: hover }"
    > 
    <span v-if="hover">
      <div class="above_pannel">按本场贡献值排序，100金瓜子=1贡献值</div>
      <div class="infinite-list-wrapper" style="overflow:auto">
        <el-scrollbar class="el-scrollbar__wrap">
        <dd v-for="(item,index) in list" :key="index">{{ item }}</dd>
        <div v-if="loading">tips：滚动加载更多</div>
        <div v-else>已无更多</div>
        </el-scrollbar>
      </div>
      <div class="below_pannel">投喂后可查看自己的排名</div>
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
        list: [1,2,3,4,5,6,7,8,9,10,11,12,13,14],
        loading: false,
        nowPage: 1,
        scrollHeight:0,
      }
    },
    mounted() {
      this.init()
      window.addEventListener("scroll",() => {
        const scrollY = document.documentElement.scrollTop || document.body.scrollTop;
        const vh = document.compatMode === "CSS1Compat" ? document.documentElement.clientHeight : document.body.clientHeight;
        const allHeight = Math.max(document.body.scrollHeight, document.documentElement.scrollHeight);
        if(scrollY + vh >= allHeight) {
          this.scrollMore()
        }
      })
    },
    methods: {
      init() {
        this.$axios.get("http://jsonplaceholder.typicode.com/posts").then(res=>{
          if(res.data.length <= 10) {
            this.list = res.data;
            this.loading = false;
          }
          else {
            this.list = res.data.slice(0, 10);
            this.loading = true;
          }
        })
      },
      scrollMore() {
        this.$axios.get("http://jsonplaceholder.typicode.com/posts").then(res =>{
          this.list = this.list.concat(res.data.slice(this.nowPage * 10, (this.nowPage + 1) * 10));
          this.nowPage++;
          if(res.data.length >= this.nowPage * 10) {
            this.loading = true;
          }
          else {
            this.loading = false;
          }
        })
      }
    }
  }
</script>

<style >
.infinite-list-wrapper {
  height: 100px;
}
.el-scrollbar {
  height: 100%;
}
.el-scrollbar__wrap {
  overflow: auto;
  overflow-x: hidden;
}
.above_pannel {
  font-size: 13px;
  color: rgb(80, 112, 119);
} 
.below_pannel {
  position: relative;
  padding: 5px 7px;
  text-align: center;
  border: 1px solid rgb(226, 225, 225);
  border-radius: 3px;
  box-sizing: border-box;
  background: #fff;
  font-size: 15px;
}
</style>


