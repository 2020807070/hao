<template>
  <article-card style="padding: 0;">
    <div slot="card-content">
      <div class="author-card">
        <div class="author-card-bg">
          <img
            class="author-card-head"
            :src="$page.frontmatter.head || 'https://avatars1.githubusercontent.com/u/24643401?s=460&v=4'"
            alt="coverMap"
          >
          <span class="author-card-name">{{ $page.frontmatter.name }}</span>
          <!-- @TODO 这里做成动效 -->
          <span class="author-card-des" style="-webkit-box-orient: vertical;">{{ $page.frontmatter.introduction }}</span>
        </div>
        <div class="author-card-info">
          <div class="author-info">
            <div class="info-item">
              <span>Posts</span>
              <CountUp startNum="0" :endNum="postsNum" times="10" speed="50"/>
            </div>
            <div class="info-item">
              <span>Classification</span>
              <CountUp startNum="0" :endNum="classNum" times="10" speed="50" />
            </div>
            <div class="info-item">
              <span>Tags</span>
              <CountUp startNum="0" :endNum="tagsNum" times="10" speed="50"/>
            </div>
          </div>
        </div>
      </div>
    </div>
  </article-card>
</template>

<script>
import ArticleCard from "./ArticleCard.vue";
import CountUp from "./CountUp";
export default {
  // props: {
  //   postsNum: {
  //     type: Number,
  //     default: 0
  //   },
  //   classNum: {
  //     type: Number,
  //     default: 0
  //   },
  //   tagsNum: {
  //     type: Number,
  //     default: 0
  //   }
  // },
  data() {
    return {
      postsNum: 0,
      tagsNum: 0,
      classNum: 10,
      introduction: ""
    };
  },
  components: { ArticleCard, CountUp },
  mounted() {
    if (!sessionStorage.getItem("introduction")) {
      sessionStorage.setItem(
        "introduction",
        this.$page.frontmatter.introduction
      );
    }
    setTimeout(() => {
      this.postsNum = sessionStorage.getItem("postsNum");
      this.tagsNum = sessionStorage.getItem("tagsNum");
      this.introduction = sessionStorage.getItem("introduction");
    }, 0);
  },
  computed: {
    options() {
      return {
        useEasing: true,
        useGrouping: true,
        separator: "",
        decimal: ".",
        decimalPlaces: "",
        prefix: "",
        suffix: ""
      };
    }
  }
};
</script>

<style lang="stylus" scoped>
.author-info {
  cursor: pointer;
  display: flex;

  .info-item {
    &:nth-child(1) {
      border: 0;
    }

    border-left: 1px solid rgba(0, 0, 0, .05);
    text-align: center;
    flex: 1;
    display: flex;
    flex-direction: column;
    justify-content: center;

    i {
      font-size: 20px;
    }

    span {
      font-size: 10px;
      justify-content: center;
      margin-bottom 10px
    }
  }
}

.atc-title {
  border-left: 5px solid red;
  padding-left: 5px;
}

.author-card {
    .author-card-bg {
      position relative
      width 100%
      height 200px
      background-size cover
      background-color rgba(120, 120, 120, 0.1)
      background-image url(https://southcat.net/wp-content/themes/easter/img/infobg.jpg)
      &:before {
        display block
        content: ''
        top 0
        left 0
        position absolute
        width 100%
        height 100%
        background #3e39ff06
      }
      .author-card-head {
        box-shadow: 0px 10px 30px -10px rgba(45, 55, 86, .3)
        position absolute
        border-radius 50%
        width 100px
        height 100px
        top 50%
        transform translateY(50%)
        left 20px
      }
      .author-card-name {
        bottom 10px
        position absolute
        color #fff
        left 150px
        font-weight bold
        font-size 20px
      }
      .author-card-des {
        position absolute
        color #010a13
        line-height  18px
        left 150px
        top 210px
        font-size 14px
        overflow hidden
        display -webkit-box
        -webkit-line-clamp 2
      }
    }
    .author-card-info {
      padding-top 80px

      padding-bottom 20px
    }

}
</style>