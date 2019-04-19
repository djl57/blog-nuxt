<template>
  <div class="header">
    <div class="wrap">
      <div class="brand">
        <h2 class="inline-block">DJLUN.</h2>
        <!-- <p class="desc inline-block">Thoughts, stories and ideas.</p> -->
        <p class="desc inline-block">Codes.</p>
      </div>
      <nav class="nav">
        <ul class="menu inline-block">
          <li class="inline-block item" :class="itemClass(item.active)" v-for="(item, index) in navs" :key="index"  
            @mouseover="mouseover1(index)" @mouseleave="mouseleave1(index)">
            <nuxt-link :to="'/'+item.link">{{ item.name }}</nuxt-link>
          </li>
        </ul>
        <div class="search inline-block cursor-pointer" :class="{'search-over': overSearch}" 
          @mouseover="mouseover" @mouseleave="mouseleave">
          <i class="el-icon-search"></i>
        </div>
      </nav>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      navs: [
        { name: 'home', link: '', active: false },
        { name: '分类', link: 'category', active: false },
        { name: '登录', link: 'signin', active: false },
        { name: '注册', link: 'signup', active: false }
      ],
      overSearch: false,
      overli: false
    }
  },
  methods: {
    mouseover() {
      this.overSearch = true
    },
    mouseleave() {
      this.overSearch = false
    },
    mouseover1(index) {
      for(let prop of this.navs) {
        prop.active = false
      }
      this.navs[index].active = true
      this.overli = true
    },
    mouseleave1(index) {
      for(let prop of this.navs) {
        prop.active = false
      }
      this.overli = false
    },
    itemClass(active) {
      return {
        'item-over': this.overSearch,
        'item-active': active,
        'item-no-active': this.overli && !active
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.header {
  height: 65px;
  padding: 50px 0 40px;
  letter-spacing: 1px;
  .wrap {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 40px;
    height: 65px;
    display: flex;
    justify-content: space-between;
    .brand {
      flex: 0 0 380px;
      line-height: 65px;
      .desc {
        color: #aaa;
        margin-left: 20px;
        font-size: 15px;
      }
    }
    .nav {
      flex: 1;
      text-align: right;
      text-transform: uppercase;
      .menu {
        font-size: 12px;
        line-height: 73px;
        .item {
          padding: 0 15px;
          transition: all 0.5s;
          &::after {
            content: '';
            position: absolute;
            left: 15px;
            right: 15px;
            bottom: 10px;
            height: 1px;
            transform: scaleY(0.5);
            background-color: #aaa;
            opacity: 0;
            transition: all 0.5s;
          }
        }
        .item-over {
          color: #aaa;
        }
        .item-active {
          position: relative;
          &::after {
            content: '';
            position: absolute;
            left: 15px;
            right: 15px;
            bottom: 25px;
            height: 1px;
            transform: scaleY(0.5);
            background-color: #aaa;
            opacity: 1;
            transition: all 0.5s;
          }
        }
        .item-no-active {
          transition: all 0.5s;
          color: #aaa;
        }
      }
      .search {
        font-size: 16px;
        padding: 10px;
        position: relative;
        top: 1px;
      }
      .search-over {
        border-radius: 50%;
        background-color: #eee;
      }
    }
  }
}
</style>
