<template>
  <div id="app">
    <div class="feed">
      <text-box :postList="postList"></text-box>
      <div v-if="postList.length > 0" class="post-container">
        <content-box
          v-for="(post,index) in postList"
          :date="post.date"
          :time="post.time"
          :text="post.text"
          :postList="postList"
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
  position: relative;
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
.post-container {
  display: flex;
  flex-direction: column-reverse;
  gap: 10px;
}
@media (max-width:450px) {
  .feed {
    width: 100%;
    margin: 0 15px;
  }
}
</style>
