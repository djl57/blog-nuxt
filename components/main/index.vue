<template>
  <div class="main">
    <div class="wrap">
      <div class="slide">
        <div class="box" @mouseover="boxover" @mouseleave="boxleave">
          <i class="el-icon-back left-arrow" :class="overBox?'left-over':'left-over-off'" @click="prevImg"></i>
          <img :src="img.img" width="100%" class="img" :class="{'active': index === idx}" :key="index" v-for="(img, index) in imgs">
          <div class="left">
            <div class="shade"></div>
          </div>
          <div class="right" @mouseenter="rightenter" @mouseleave="rightleave">
            <div class="shade"></div>
          </div>
          <i class="el-icon-back right-arrow" :class="overBox?'right-over':'right-over-off'" @click="nextImg" @mouseenter="rightenter" @mouseleave="rightleave"></i>
        </div>
      </div>
      <div class="content clearfix">
        <article v-for="(item, index) in articles" :key="index" class="item">
          <img :src="item.img" height="auto" width="100%">
          <div class="shade"></div>
          <div class="title">{{ item.title }}</div>
        </article>
      </div>
      <div class="page-nav">
        <i class="el-icon-back left"></i>
        <span class="page-num">{{ curPage }} / {{ totalPage }}</span>
        <i class="el-icon-back right"></i>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      curPage: 1,
      totalPage: 2,
      articles: [
        { title: '文章1', img: require('../../assets/images/cover01.jpg') },
        { title: '文章2', img: require('../../assets/images/cover02.jpg') },
        { title: '文章3', img: require('../../assets/images/cover03.jpg') },
        { title: '文章4', img: require('../../assets/images/cover04.jpg') },
        { title: '文章5', img: require('../../assets/images/cover05.jpg') },
        { title: '文章3', img: require('../../assets/images/cover08.jpg') },
        { title: '文章5', img: require('../../assets/images/cover10.jpg') },
        { title: '文章5', img: require('../../assets/images/cover11.jpg') },
        { title: '文章5', img: require('../../assets/images/cover12.jpg') }
      ],
      enterRight: false,
      overBox: false,
      imgs: [
        { title: '文章1', img: require('../../assets/images/cover04.jpg') },
        { title: '文章2', img: require('../../assets/images/cover05.jpg') },
        { title: '文章3', img: require('../../assets/images/cover08.jpg') },
      ],
      idx: 0,
    }
  },
  methods: {
    rightenter() {
      this.enterRight = true
      this.nextImg()
    },
    rightleave() {
      this.enterRight = false
      this.prevImg()
    },
    boxover() {
      this.overBox = true
    },
    boxleave() {
      this.overBox = false
    },
    prevImg() {
      if(this.idx === 0) {
        this.idx = this.imgs.length-1
      } else {
        this.idx --
      }
    },
    nextImg() {
      if(this.idx === this.imgs.length-1) {
        this.idx = 0
      } else {
        this.idx ++
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.main {
  .wrap {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 40px;
    .slide {
      margin-bottom: 40px;
      .box {
        width: 100%;
        height: 520px;
        position: relative;
        overflow: hidden;
        .img {
          z-index: -1;
          position: absolute;
          opacity: 0;
          transition: all 0.8s;
        }
        .active {
          opacity: 1;
          transition: all 0.8s;
        }
        .left, .right {
          float: left;
          width: 50%;
          height: 100%;
          position: relative;
          .shade {
            position: absolute;
            top: 0;
            bottom: 0;
            left: 0;
            right: 0;
            background-color: rgba($color: #000000, $alpha: 0.3);
            transition: all 0.3s;
          }
          .title {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate3d(-50%, -50%, 0);
            color: #ffffff;
            z-index: 2;
            font-size: 25px;
          }
        }
        .left {
          box-sizing: border-box;
          border-right: 1px solid #fff;
        }
        .left-arrow, .right-arrow {
          position: absolute;
          top: 50%;
          transform: translateY(-50%);
          color: #fff;
          transition: all 0.5s;
          z-index: 1;
          cursor: pointer;
          padding: 10px;
        }
        .right-arrow {
          transform: rotateZ(180deg);
        }
        .left-over-off {
          left: -25px;
        }
        .right-over-off {
          right: -25px;
        }
        .left-over {
          left: 40px;
          transition: all 0.5s;
        }
        .right-over {
          right: 40px;
          transition: all 0.5s;
        }
      }
    }
    .content {
      margin: 0 -20px;
      .item {
        box-sizing:border-box;
        float: left;
        margin-bottom: 40px;
        padding: 0 20px;
        height: 350px;
        vertical-align: top;
        width: calc(100%/2);
        overflow: hidden;
        position: relative;
        cursor: pointer;
        .shade {
          position: absolute;
          top: 0;
          bottom: 0;
          left: 20px;
          right: 20px;
          background-color: rgba($color: #000000, $alpha: 0.3);
          transition: all 0.3s;
          z-index: 1;
          &:hover {
            background-color: rgba($color: #000000, $alpha: 0.6);
            transition: all 0.3s;
          }
        }
        .title {
          position: absolute;
          top: 50%;
          left: 50%;
          transform: translate3d(-50%, -50%, 0);
          color: #ffffff;
          z-index: 2;
          font-size: 25px;
        }
      }
    }
    .page-nav {
      text-align: center;
      margin: 30px auto 60px;
      .page-num {
        font-size: 22px;
        padding: 0 10px;
        color: #330;
      }
      .left, .right {
        cursor: pointer;
        padding: 10px;
      }
      .right {
        transform: rotateZ(180deg);
      }
    }
  }
}
</style>
