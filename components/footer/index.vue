<template>
  <div class="footer">
    <div class="wrap">
      <div class="left">
        <p class="ft-title">推 荐</p>
        <ul>
          <li v-for="(item, index) in recom" :key="index" class="item">
            <a :href="item.link">{{ item.name }}</a>
          </li>
        </ul>
      </div>
      <div class="middle">
        <p class="ft-title">资 源</p>
        <ul>
          <li v-for="(item, index) in sourse" :key="index" class="item">
            <a :href="item.link">{{ item.name }}</a>
          </li>
        </ul>
      </div>
      <div class="right">
        <p class="ft-title">联 系 我</p>
        <div class="get" :class="showEmail?'email':'no-email'" @click="getEmail">{{ email }}</div>
      </div>
    </div>
    <div class="copyright">
      Copyright © {{ new Date().getFullYear() }} - <span class="author">DJLUN.</span>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      recom: [
        { link: 'https://unsplash.com/', name: 'unsplash' },
        { link: 'https://marketplace.ghost.org/', name: 'ghost' },
        { link: 'https://www.iconfont.cn/', name: 'iconfont' },
      ],
      sourse: [
        { link: 'https://github.com/djl57/blog-nuxt', name: 'github' },
      ],
      showEmail: false,
      email: '获 取'
    }
  },
  methods: {
    getEmail() {
      this.showEmail = !this.showEmail
      this.showEmail ? this.email = 'djl5700@163.com' : this.email = '获 取'
    }
  }
};
</script>

<style lang="scss" scoped>
.footer {
  border-top: 1px solid #eee;
  .wrap {
    max-width: 1200px;
    margin: 0 auto;
    display: flex;
    padding: 0 40px;
    .left,
    .middle,
    .right {
      flex: 1;
      .ft-title {
        color: #aaa;
        font-size: 14px;
        letter-spacing: 2px;
        padding-bottom: 20px;
        font-weight: 600;
      }
      .item {
        height: 32px;
        line-height: 32px;
        color: #330;
      }
    }
    .left {
      padding: 60px 60px 60px 0;
    }
    .middle {
      border-left: 1px solid #eee;
      border-right: 1px solid #eee;
      padding: 60px;
    }
    .right {
      padding: 60px 0 60px 60px;
      .get {
        width: 100%;
        height: 30px;
        line-height: 30px;
        font-size: 12px;
        text-align: center;
        cursor: pointer;
      }
      .no-email {
        color: #fff;
        background-color: #330; 
        transition: background-color 0.75s;
      }
      .email {
        color: #330;
        background-color: #fff; 
        border: 1px solid #330;
        transition: background-color 0.75s;
      }
    }
  }
  .copyright {
    border-top: 1px solid #eee;
    color: #aaa;
    font-size: 11px;
    padding: 30px 0;
    text-align: center;
    text-transform: uppercase;
    .author {
      color: #330;
    }
  }
}
</style>
