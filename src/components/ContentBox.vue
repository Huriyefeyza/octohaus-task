<template>
  <div class="content-box">
    <div class="top-content">
      <div class="profile-image">
        <img src="../assets/profile.png" />
      </div>
      <div class="content">
        <div class="date">{{date}} - {{time}}</div>
        <div class="text">
          <span class="name">Jane Doe </span>{{text}}
        </div>
      </div>
    </div>
    <div class="bottom">
      <div class="left-content">
        <div class="like" @click="likePost" :class="{active : like.active}">
          <i data-feather="thumbs-up"></i>
          <span>{{like.count}}</span>
        </div>
        <div class="dislike" @click="dislikePost" :class="{active : dislike.active}">
          <i data-feather="thumbs-down"></i>
          <span>{{dislike.count}}</span>
        </div>
      </div>
      <div class="right-content">
        <div class="edit">
          <i data-feather="edit-3"></i>
        </div>
        <div class="trash" @click="trashElement">
          <i data-feather="trash-2"></i>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import feather from "feather-icons";
export default {
  props: ["date","time", "text", "postList"],
  mounted() {
    feather.replace();
  },
  data(){
    return {
      like: {
        count: 0,
        active: false,
      },
      dislike: {
        count: 9,
        active: false,
      }
    }
  },
  methods: {
    trashElement() {
      let index = this.$vnode.key;

      const postList = this.postList
      postList.splice(index,1)

      window.localStorage.setItem('postList', JSON.stringify(postList))

    },
    likePost() {
      this.like.active = !this.like.active
      this.like.active ? this.like.count++ : this.like.count--
    },
    dislikePost() {
      this.dislike.active = !this.dislike.active
      this.dislike.active ? this.dislike.count++ : this.dislike.count--
    }
  }
};
</script>
<style>
.content-box {
  box-shadow: 0px 3px 6px #00000029;
  border-radius: 5px;
  background-color: #fff;
  width: 100%;
  margin: 19px 0;
}
.content-box .top-content {
  border-bottom: 1px solid #eaecee;
  padding: 20px 20px 19px;
  display: flex;
  gap: 10px;
}
.content-box .right-content {
  display: flex;
  align-items: center;
  gap: 10px;
}
.content-box .bottom {
  padding: 13px 20px;
}
.content-box .content {
  text-align: start;
}
.content-box svg {
  margin-right: 0;
}
.profile-image {
  width: 40px;
  height: 40px;
  flex-shrink: 0;
}
.profile-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.text {
  color: #5d6d7e;
  line-height: 16px;
  font-size: 14px;
}
.name {
  color: #9b59b6;
  font-weight: 500;
}
.date {
  color: #99a4ae;
  font-size: 8px;
}
.left-content{
  display: flex;
  align-items: center;
}
.like,
.dislike {
  display: flex;
  align-items: center;
  gap: 5px;
  margin-right: 20px;
  cursor: pointer;
}
.left-content span{
  color: #C1C8CE;
  font-size: 14px;
}
.active svg,
.active span{
  color: #34495E !important
}
</style>
