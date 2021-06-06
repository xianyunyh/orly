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
      <div class='pic-top'></div>
      <div class="top-text">
        {{top_text}}
      </div>
      <div class="img-box"> <img src="/img/0.tif.56a5ab37.gif" alt=""></div>
      <div class="main-title">
        {{main_title}}
      </div>
      <div class="extra-title">
        {{extra_title}}
      </div>
      <div class="foot">
        <div class="foot-left">O'RLY?</div>
        <div class="author-text">{{author}}</div>
      </div>
    </div>
    <a :href="imgSrc" target="_blank" download>{{$t("download")}}</a>

  </div>
</template>

<script>
  export default {
    name: "Result",
    props: {
      inputSrc: String,
    },
    beforeMount: function() {
      this.imgSrc = this.inputSrc
    },
    data: function () {
      return {
        baseURL: process.env.BASE_URL,
        imgSrc: "",
        top_text: "Top Text 顶部文字",
        main_title: "Title 标题",
        extra_title: "Guid Title副标题",
        foot_left_text: "O'RLY?",
        author: "Author 作者"
      }
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
    margin-top: 10px;
    padding-left: 70px;
  }
  .pic-top {
    margin: 0 auto;
    width: 360px;
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
    font-size: 56px;
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
    box-shadow: 10px 10px 20px #999;
  }
  .pic-area img {
    width: 280px;
    height: 280px;
    margin-left: 30px;
  }
  .foot{
    display: flex;
    justify-content: space-between;
    margin-top: 60px;
    padding: 0 25px;
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