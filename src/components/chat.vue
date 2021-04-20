<template>
  <div ref="editor" class="editor">
    <div
      ref="editorContent"
      class="editor-content"
      contenteditable="true"
      @keydown.prevent.enter.exact="onEnter"
    ></div>
    <el-button class="send-btn" @click="sendMsg">发送</el-button>
    <el-button class="del-btn" @click="delMsg">清除</el-button>
  </div>
</template>

<script>
export default {
  methods: {
    sendMsg() {
      const el = this.$refs.editorContent;
      const childNodes = [...el.childNodes];
      this.$emit("send-message", childNodes, el.innerHTML);
      el.innerHTML = "";
    },
    delMsg() {
      console.log("test del");
      this.$emit("del-message");
    },
    // 监听enter事件
    onEnter(e) {
      const el = this.$refs.editorContent
      if (this.memberListVisible) {
        e.preventDefault();
        const selectedMember = this.matchedMembers.find(item => item.selected);
        console.log(selectedMember);
        this.insertMention(selectedMember.name, selectedMember.id);
        this.memberListVisible = false;
        selectedMember.selected = false;
      } 
      else if (el.innerHTML) {
        this.sendMsg();
      }
    },
  }
}
</script>

<style>
.editor {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: left;
  border: 1px solid #acacac;
  border-radius: 3px;
  box-sizing: border-box;
}
.editor-content {
  width: 75%;
  min-width: 200px;
  height: 80%;
  min-height: 20px;
  padding: 3px 5px;
  outline: none;
  background: #ffffff ;
}
.send-btn {
  position: absolute;
  bottom: 2px;
  right: 60px;
}
.del-btn {
  position: absolute;
  bottom: 2px;
  right: 10px;
}
</style>