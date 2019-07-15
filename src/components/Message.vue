<template>
  <div class="message">
    <div class="panel">
      <div class="head">
        <router-link
          to="/"
          class="head-home"
        >主页</router-link>
        <span>/ 新消息</span>
      </div>
      <div
        class="cell"
        v-for="hasNotMessage in hasNotMessages"
        :key="hasNotMessage.id"
      >
        <router-link
          class="title"
          :to="`/user/${hasNotMessage.author.loginname}`"
        >{{hasNotMessage.author.loginname}}</router-link>
        <span class="padding-lr">回复了你的话题</span>
        <router-link
          class="title"
          :to="`/topics/${hasNotMessage.topic.id}`"
        >{{hasNotMessage.topic.title}}</router-link>
      </div>
      <div
        class="cell more"
        v-if="!hasNotMessages.length"
      >无话题</div>
    </div>
    <div class="panel">
      <div class="head">过往信息</div>
      <div
        class="cell"
        v-for="hasMessage in hasMessages"
        :key="hasMessage.id"
      >
        <router-link
          class="title"
          :to="`/user/${hasMessage.author.loginname}`"
        >{{hasMessage.author.loginname}}</router-link>
        <span class="padding-lr">{{hasMessage.type==='at'?'在话题':'回复了你的话题'}}</span>
        <router-link
          class="title"
          :to="`/topics/${hasMessage.topic.id}`"
        >{{hasMessage.topic.title}}</router-link>
        <span class="padding-lr">{{hasMessage.type==='at'?'中@了你':''}}</span>
        <div class="time">
          <img
            src="https://www.vue-js.com/public/images/checkmark_icon&16.png"
            alt
          />
        </div>
      </div>
      <div
        class="cell more"
        v-if="!hasMessages.length"
      >无话题</div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "message",
  data() {
    return {
      hasMessages: [],
      hasNotMessages: []
    };
  },
  created() {
    axios
      .get(
        `https://www.vue-js.com/api/v1/messages?accesstoken=${sessionStorage.getItem(
          "token"
        )}`
      )
      .then(res => {
        this.messageNum = res.data.data;
        console.log(res.data);
        this.hasMessages = res.data.data.has_read_messages;
        this.haNotMessages = res.data.data.hasnot_read_messages;
        // 将得到的信息存储到本地浏览器
      });
  }
};
</script>

<style>
.message {
  width: 90%;
  margin: 0 auto;
  margin-top: 20px;
}
.message .padding-lr {
  padding: 0 5px;
}
.message .panel .cell img {
  width: 16px;
}
</style>