<template>
  <div
    class="user"
    v-if="user"
  >
    <div class="panel">
      <div class="head">
        <router-link
          to="/"
          class="head-home"
        >主页</router-link>
        <span>/</span>
      </div>
      <div class="userinfo">
        <div>
          <img
            :src="user.avatar_url"
            alt
          />
          <span>{{user.loginname}}</span>
        </div>
        <div>{{user.score}} 积分</div>
        <div>注册时间 {{myMomentTime(user.create_at)}}</div>
      </div>
    </div>
    <div class="panel">
      <div class="head">最近创建的话题</div>
      <div
        class="cell"
        v-for="recent_topic in user.recent_topics"
        :key="recent_topic.id"
      >
        <router-link :to="`/user/${recent_topic.author.loginname}`">
          <img
            :src="recent_topic.author.avatar_url"
            alt
          />
        </router-link>
        <!-- <div class="count">
          <span class="reply-count">{{recent_topic.reply_count}}</span>/
          <span class="visit-count">{{recent_topic.visit_count}}</span>
        </div>-->
        <router-link
          :to="`/topics/${recent_topic.id}`"
          class="title"
        >{{recent_topic.title}}</router-link>
        <span class="time">{{myMomentTime(recent_topic.last_reply_at)}}</span>
      </div>
      <div
        class="cell more"
        v-if="user.recent_topics.length"
      >查看更多》</div>
      <div
        class="cell more"
        v-else
      >无话题</div>
    </div>
    <div class="panel">
      <div class="head">最近参与的话题</div>
      <div
        class="cell"
        v-for="recent_replie in user.recent_replies"
        :key="recent_replie.id"
      >
        <router-link :to="`/user/${recent_replie.author.loginname}`">
          <img
            :src="recent_replie.author.avatar_url"
            alt
          />
        </router-link>
        <!-- <div class="count">
          <span class="reply-count">{{recent_replie.reply_count}}</span>/
          <span class="visit-count">{{recent_replie.visit_count}}</span>
        </div>-->
        <router-link
          :to="`/topics/${recent_replie.id}`"
          class="title"
        >{{recent_replie.title}}</router-link>
        <span class="time">{{myMomentTime(recent_replie.last_reply_at)}}</span>
      </div>
      <div
        class="cell more"
        v-if="user.recent_replies.length"
      >查看更多》</div>
      <div
        class="cell more"
        v-else
      >无话题</div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import moment from "moment";
export default {
  name: "user",
  data() {
    return {
      user: null
    };
  },
  watch: {
    "$route.fullPath": {
      immediate: true,
      handler() {
        const loginname = this.$route.params.loginname;
        axios
          .get(`https://www.vue-js.com/api/v1/user/${loginname}`)
          .then(res => {
            this.user = res.data.data;
            // console.log(res.data.data);
          });
      }
    }
  },
  // created() {
  //   const loginname = this.$route.params.loginname;
  //   axios.get(`https://www.vue-js.com/api/v1/user/${loginname}`).then(res => {
  //     this.user = res.data.data;
  //     console.log(res.data.data);
  //   });
  // },
  methods: {
    myMomentTime(time) {
      moment.locale("zh-cn");
      return moment(time).fromNow();
    }
  }
};
</script>

<style>
.user {
  width: 90%;
  margin: 0 auto;
  margin-top: 20px;
}
.panel {
  margin-bottom: 13px;
}
.user .userinfo {
  padding: 10px;
  border-top: 1px solid #e5e5e5;
  line-height: 2em;
  background-color: #fff;
  border-radius: 0 0 3px 3px;
}
.user .userinfo img {
  width: 40px;
  border-radius: 2px;
}
.panel .head .head-home {
  color: #369219;
}
.panel .head {
  padding: 10px;
  background-color: #f6f6f6;
  border-radius: 3px 3px 0 0;
  color: #1c6132;
}
.panel .cell {
  display: flex;
  overflow: hidden;
  padding: 10px 0 10px 10px;
  font-size: 14px;
  padding-right: 10px;
  background: #fff;
  border-top: 1px solid #f0f0f0;
  align-items: center;
}
.panel .cell img {
  width: 30px;
  border-radius: 2px;
}
.panel .cell .title {
  padding-left: 5px;
  color: #08c;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
.panel .cell .title:hover {
  color: #005580;
  text-decoration: underline;
}
.panel .cell .time {
  flex-shrink: 0;
  flex-grow: 1;
  text-align: right;
}
.user .panel .cell-more {
  padding: 10px;
}
</style>