<!--
  - Copyright (c) 2018 LI Zhennan
  -
  - Use of this work is governed by an MIT License.
  - You may find a license copy in project root.
  -
  -->

<template>
  <div class="result">
    <!-- <progressive-img
      class="img"
      :blur="3"
      :src="imgSrc"
      :placeholder="baseURL + 'example.gif'"
      :fallback="baseURL + 'error.gif'"
      alt="Your O'RLY Book Cover"
    ></progressive-img> -->
    
    <div class="pic-area">
      <div class='pic-top' v-bind:style="{ backgroundColor: bgColor }"></div>
      <div class="top-text">
        {{input.topText}}
      </div>
      <div class="img-box"> <img :src="animalPic" alt=""></div>
      <div class="main-title" v-bind:style="{ backgroundColor: bgColor }">
        {{input.title}}
      </div>
      <div class="extra-title">
        {{input.guideText}}
      </div>
      <div class="foot">
        <div class="foot-left">O'RLY?</div>
        <div class="author-text">{{input.author}}</div>
      </div>
    </div>
    <a :href="imgSrc" target="_blank" download>{{$t("download")}}</a>

  </div>
</template>

<script>
  import bus from '@/bus';

  export default {
    name: "Result",
    props: {
      inputSrc: String,
      colors: Array,
    },
    beforeMount: function() {
      this.imgSrc = this.inputSrc
    },
    data: function () {
      return {
        input: {
          title: 'Title 标题',
          topText: 'Top Text 顶部文字',
          guideText: 'Guid Title副标题',
          author: 'Author 作者'
        },
        baseURL: process.env.BASE_URL,
        imgSrc: ""
      }
    },
    mounted(){
      bus.$on('message', (e) => {
        this.input = {...this.input,...e}
      })
      bus.$on('animal', (e) => {
        console.log(e)
        this.input.animalCode = e
      })
    },
    computed: {
      bgColor(){
        const index = this.input.colorCode < 0 ? 0 : parseInt(this.input.colorCode,10) 
        const item = this.colors[index]
        return item
      },
      animalPic() {
        const index = 3
        console.log(index)
        return require(`../assets/thumbnails/${index}.tif.gif`);
    },
    },
    watch: {
      inputSrc: function (newVal) {
        if (newVal === this.imgSrc) {
          return
        }
        this.imgSrc = newVal
      }
    },
  }
</script>

<style scoped>
  .result {
    width: 400px;
  }
  .img-box {
    padding: 0 16px;
    height: 280px;
  }
  .pic-top {
    margin: 0 auto;
    width: 368px;
    background: #888888;
    height: 8px;
  }
  .main-title {
    width: 360px;
    height: 110px;
    margin: 0 auto;
    background: #777777;
    text-align: left;
    line-height: 110px;
    font-size: 58px;
    color: #fff;
    padding-left: 10px;
    font-weight: bold;
  }
  .extra-title{
    text-align: right;
    font-weight: bold;
    font-size: 17px;
    margin: 5px  18px 0 0 ;


  }
  .pic-area {
    width: 400px;
    height: 560px;
    position: relative;
    box-shadow: 10px 10px 20px #999;
  }
  .pic-area img {
    padding: 0 16px;
    height: 100%;
  }
  .foot{
    position: absolute;
    display: flex;
    justify-content: space-between;
    width: 100%;
    margin-top: 60px;
    padding: 0 25px;
    bottom: 18px;
  }
  .author-text{
    font-size: 13px;
    font-weight: bold;
  }
  @media screen and (min-width: 970px) {
    .result {
      margin: 20px 0 0 50px;
    }
  }
  @media screen and (max-width: 970px) {
    .result {
      margin: 30px 50px 0 50px;
    }
  }
  @media screen and (max-width: 401px) {
    .result {
      max-width: 96%;
      margin: 30px 0 0 0;
    }
  }
  .img, img, a {
    -webkit-appearance: none;
    outline: none;
    display: block;
    width: 100%;
  }
  .img div {
    width: 100%;
  }
  a {
    white-space: nowrap;
    margin: 20px 0 0 0;
    font-size: 1.2em;
    padding: 12px;
    background: black;
    color: white;
    border: none;
    font-weight: bold;
    text-decoration: none;
  }
  a:active {
    background: white;
    color: black;
    box-shadow: 0 0 0 2px black inset;
  }
  .img {
    box-shadow: 8px 8px 30px black;
  }

</style>