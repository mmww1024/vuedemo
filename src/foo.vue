<template>
  <div class="wrapper">
    <header :newsInfo="newsInfo"></header>
    <content :contentList="contentList"></content>
    <related :recommendList="recommendList"></related>
    <hot-reviews :topComment="topComment"></hot-reviews>
    <latest-reviews :newComment="newComment"></latest-reviews>
  </div>
</template>

<style lang="sass" src="../assets/sass/index.scss"></style>

<script>
  var stream = weex.requireModule('stream');
  // import axios from 'axios';
  import header from './news/header.vue';
  import content from './news/content.vue';
  import related from './news/related.vue';
  import hotReviews from './news/hotReviews.vue';
  import latestReviews from './news/latestReviews.vue';
  export default {
    components:{
      header,content,related,hotReviews,latestReviews
    },
    created:function(){
      this.init( response => { 
        console.log(response)
        // this.title=response.data.country;

        // this.msg=response.data.data.errorMsg
        console.log(response.data.status)
        if(response.data.status){
            this.resdata = response.data.data;
            this.newsInfo = this.resdata.newsInfo;
            this.contentList = this.resdata.contentList;
            this.recommendList = this.resdata.recommendList;
            this.topComment = this.resdata.topComment;
            this.newComment = this.resdata.newComment;
        }
      });
    },
    data: function(){
      return {
        newsInfo:{},
        contentList:[],
        recommendList:[],
        topComment:[],
        newComment:[],
      };
    },
    methods: {
      init: function (callback) {
        return stream.fetch({
          method: 'GET',
          type: 'json',
          // url:'https://api.github.com/repos/vuejs/vue'
          // url:'http://api.zippopotam.us/us/90210'
          // url:'https://mp.xcar.com.cn/series/brand-list'
          url: '../src/data.json'
        }, callback)
      },
      // deepClone: function(data) {
      //   let newObj = _.isArray(data) ? [] : ( _.isObject(data) ? {} : data);
      //   if (data instanceof Object) {
      //     for (let key in data) {
      //       newObj[key] = this.deepClone(data[key]);
      //     }
      //   }

      //   return newObj;
      // }
      

    }
  }
</script>
