<template>
  <div class="explore-unit">
    <div class="result-unit" @click="gotoArticle">
      <div class="content-unit">
        <h1 v-if="paperData.highlight && paperData.highlight.title" v-html="paperData.highlight.title[0]" class="unit-title">
        </h1>
        <!-- 当 highlight.title 不存在时，直接显示 title -->
        <!-- 论文题目 -->
        <h1 v-else class="unit-title">
          {{ this.paperData._source.title }}
        </h1>
        <!-- 作者 -->
        <div class="unit-author">
          <i class="el-icon-user-solid">
            &nbsp;
            <span v-for="(name,index) in paperData._source.authorships" :key="index">
              {{name.author.display_name}}&nbsp;
              <span v-if="index < paperData._source.authorships.length - 1">,&nbsp;&nbsp;</span>
            </span>
          </i>
        </div>
        <!-- 论文摘要 -->
        <div class="unit-preview">
          论文摘要：{{ this.abstract }}
        </div>
        <!-- 来源期刊 -->
        <div class="unit-periodical">
          来源期刊:《{{ this.journal }}》
        </div>
        <div class="unit-keywords">
          <span>关键词:</span> <span v-for="(keyword, index) in this.paperData._source.keywords" :key="index">
            {{ keyword.keyword }} <span v-if="index < paperData._source.keywords.length-1"></span>
          </span>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "ExploreUnit",
  props: {
    paperData: {

    }
  },
  data() {
    return {
      id: '',
      isOverflow: true,
      journal: 'unknown',
      abstract: 'unknown'
    };
  },
  methods: {
    gotoArticle() {
      this.$router.push("/article/" + btoa(encodeURIComponent(JSON.stringify(this.paperData._id))));
    },
  },
  created() {
    console.log(this.paperData)
    if (this.paperData._source.primary_location) {
      this.journal = this.paperData._source.primary_location.source.display_name
    }
    if (this.paperData._source.abstract_inverted_index) {
      this.abstract = this.paperData._source.abstract_inverted_index
    }
  }
};
</script>
<style scoped>
.explore-unit {
  background-color: rgb(226, 239, 255);
  width: 95%;
  min-height: 135px;
  max-height: 300px;
  /* padding: 10px; */
  display: block;
  margin: 4px 15px;
  padding: 10px;
  font-family: Inter, Roboto, pingfang SC, hiragino sans gb, Apple SD Gothic Neo, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, sans-serif, helvetica neue, arial, microsoft yahei ui, microsoft yahei, Apple Color Emoji, Segoe UI Emoji, Segoe UI Symbol, Noto Color Emoji;
  box-shadow: 1px 1px rgba(0, 0, 0, 0.3);
  margin-bottom: 10px;
  transition: box-shadow 0.7s;
}

.explore-unit:hover {
  background-color: rgb(221, 236, 255);
  width: 95%;
  min-height: 140px;
  max-height: 240px;
  /* padding: 10px; */
  display: block;
  margin: 5px 15px;
  padding: 10px;
  font-family: Inter, Roboto, pingfang SC, hiragino sans gb, Apple SD Gothic Neo, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, sans-serif, helvetica neue, arial, microsoft yahei ui, microsoft yahei, Apple Color Emoji, Segoe UI Emoji, Segoe UI Symbol, Noto Color Emoji;
  box-shadow: 7px 7px rgba(0, 0, 0, 0.2);
  margin-bottom: 20px;
}

.content-unit {
  padding: 0 40px 15px 10px;
}

.unit-title {
  font-size: 25px;
  color: #2f3a91;
  font-weight: 600;
  font-synthsis: style;
  line-height: 2.0;
  margin-left: 20px;
  text-align: left;
  max-width: 800px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  word-break: break-word;
  cursor: pointer;
}

.unit-author {
  display: flex;
  flex-direction: column;
}

.unit-author i {
  overflow: hidden;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 2;
  /* 控制显示的行数 */
  white-space: normal;
  line-height: 1.2;
  width: 90%;
  text-align: left;
  margin-left: 20px;
  font-weight: 700;
}

.unit-author i span {
  font-size: 15px;
  -webkit-line-clamp: 1;
  /* 控制显示的行数 */
}

.unit-author i span:hover {
  /* text-decoration: underline; */
  border-bottom: 1px dashed;
  /* 虚线下划线 */
}

.unit-preview {
  font-size: 15px;
  padding-top: 5px;
  width: 90%;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  overflow: hidden;
  -webkit-line-clamp: 4;
  /* 控制显示的行数 */
  font-weight: 400;
  text-align: left;
  margin-left: 20px;
  color: #7e7979;
}

.unit-periodical {
  font-size: 15px;
  padding-top: 5px;
  width: 90%;
  text-align: left;
  margin-left: 20px;
  font-weight: 400;
}

.unit-keywords {
  margin-top: 10px;
  overflow: hidden;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 2;
  /* 控制显示的行数 */
  white-space: normal;
  line-height: 1.2;
  width: 90%;
  text-align: left;
  margin-left: 20px;
  font-weight: 400;
}

.unit-keywords:hover {
  color: #7e7979;
}

.unit-source {
  color: rgba(128, 124, 124, 0.999);
}

.unit-preview {
  font-size: 15px;
  padding-top: 5px;
  width: 100%;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  overflow: hidden;
  -webkit-line-clamp: 4;
  /* 控制显示的行数 */
  font-weight: 400;
  text-align: left;
  /* 设置文本靠左对齐 */
}

.unit-preview:hover {
  color: #7e7979;
}
</style>
