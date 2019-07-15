<template>
  <footer>
    <div class="footer-inner">
      <div class="links">RSS | 源码地址</div>
      <div class="col-fade">
        <P>
          服务器搭建在
          <a href="http://www.ucloud.cn/?utm_source=zanzhu&amp;utm_campaign=Ionichina&amp;utm_medium=display">
            <img
              src="https://www.vue-js.com/public/images/ucloud.png"
              alt
            />
          </a>
          存储赞助商为
          <a
            href="http://www.qiniu.com/?ref=ionichina"
            target="_blank"
            class="sponsor_outlink"
            data-label="qiniu_bottom"
          >
            <img
              src="https://www.vue-js.com/public/images/qiniu.png"
              alt
            />
          </a>
        </P>
        <P>声明：内容均来自于网络，如有侵权行为请发送邮件至vueclub@126.com,我们将在第一时间删除</P>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: "foot"
};
</script>

<style>
footer {
  background-color: #fff;
  margin-top: 50px;
}
footer .footer-inner {
  width: 90%;
  margin: 0 auto;
  padding: 20px 0;
  font-size: 14px;
  color: #807a7a;
}
footer .footer-inner .links {
  color: #666;
  font-style: 13px;
}
footer .footer-inner .col-fade p img {
  height: auto;
  max-width: 100%;
  vertical-align: middle;
  border: 0;
}
footer .footer-inner .col-fade p {
  line-height: 20px;
}
</style>