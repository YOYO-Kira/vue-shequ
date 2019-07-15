<template>
  <div class="create">
    <div class="panel postion">
      <div class="head">
        <router-link
          to="/"
          class="head-home"
        >主页</router-link>
        <span>/</span>
      </div>
      <div class="tab-selector">
        <span>选择板块：</span>
        <select
          name="tab"
          id="tab-value"
          v-model="tab"
        >
          <option value>请选择</option>
          <!-- <option value="weex">weex</option> -->
          <option value="share">分享</option>
          <option value="ask">问答</option>
          <option value="job">招聘</option>
        </select>
      </div>
      <div class="post">
        <input
          type="text"
          placeholder="标题字数10字以上"
          v-model="title"
        />
        <!-- <textarea v-model="content"></textarea> -->
        <quill-editor
          v-model="content"
          ref="myQuillEditor"
          :options="editorOption"
          @blur="onEditorBlur($event)"
          @focus="onEditorFocus($event)"
          @ready="onEditorReady($event)"
        ></quill-editor>
        <button @click="createTopic">提交</button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import "quill/dist/quill.core.css";
import "quill/dist/quill.snow.css";
import "quill/dist/quill.bubble.css";
import { quillEditor } from "vue-quill-editor";
export default {
  name: "createtopic",
  components: {
    quillEditor
  },
  data() {
    return {
      title: "",
      content: "",
      tab: "",
      editorOption: {}
      //  父文本编辑器的配置
    };
  },
  methods: {
    createTopic() {
      axios
        .post("https://www.vue-js.com/api/v1/topics", {
          title: this.title,
          tab: this.tab,
          content: this.content,
          accesstoken: sessionStorage.getItem("token")
        })
        .then(res => {
          console.log(res.data);
          this.title = "";
          this.content = "";
          this.tab = "";
          this.$router.push(`/topics/${res.data.topic_id}`);
        });
    },
    onEditorBlur(quill) {
      console.log("editor blur!", quill);
    },
    onEditorFocus(quill) {
      console.log("editor focus!", quill);
    },
    onEditorReady(quill) {
      console.log("editor ready!", quill);
    },
    onEditorChange({ quill, html, text }) {
      console.log("editor change!", quill, html, text);
      this.content = html;
      //  当父文本编辑器输入内容时，同步修改自己的data
    }
  }
};
</script>

<style>
.create {
  width: 90%;
  margin: 0 auto;
  margin-top: 20px;
}
.create .tab-selector,
.post {
  background-color: #fff;
  padding: 15px;
  border-bottom: 1px solid #ccc;
}
.create select {
  width: 220px;
  background-color: #fff;
  border: 1px solid #ccc;
  height: 30px;
  line-height: 30px;
  border-radius: 4px;
}
.create input {
  width: 100%;
  border: 1px solid #ccc;
  border-radius: 4px;
  line-height: 25px;
  padding-left: 5px;
  outline: none;
  margin-bottom: 15px;
}
.create .panel textarea {
  height: 500px;
}
.create .post button {
  left: 70px;
  bottom: -45px;
}
.create .ql-editor {
  height: 500px;
}
</style>