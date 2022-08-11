<template>
  <div id="app">
    <div class="feed">
      <text-box :postList="postList"></text-box>
      <div v-if="postList.length > 0">
        <content-box
          v-for="(post,index) in postList"
          :date="post.date"
          :time="post.time"
          :text="post.text"
          :key="index"
        ></content-box>
      </div>
    </div>
  </div>
</template>

<script>
import TextBox from "./components/TextBox.vue";
import ContentBox from "./components/ContentBox.vue";
export default {
  name: "App",
  components: {
    TextBox,
    ContentBox,
  },
  data() {
    return {
      postList: [],
    };
  },
  created() {
    this.postList = window.localStorage.getItem("postList")
      ? JSON.parse(window.localStorage.getItem("postList"))
      : this.postList;
      console.log(this.postList);
      console.log(this.postList.length)
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@400;500&display=swap");
body {
  width: 100%;
  min-height: 100%;
  background-color: #34495e;
  overflow-x: hidden;
}
* {
  font-family: "Roboto", sans-serif;
  margin: 0;
  padding: 0;
  font-weight: 400;
}
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.feed {
  width: 420px;
  margin: auto;
}
</style>
