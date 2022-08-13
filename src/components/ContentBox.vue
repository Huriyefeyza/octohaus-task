<template>
  <div class="content-box" :style="{zIndex: editShow ? 1 : 0}">
    <div class="top-content">
      <div class="profile-image">
        <img src="../assets/profile.png" />
      </div>
      <div class="content">
        <div class="date">{{ date }} - {{ time }}</div>
        <div class="text" v-if="!editShow">
          <span class="name">Jane Doe </span> {{ text }}
        </div>
        <div class="text" v-else>
          <span class="name">Jane Doe </span>
          <div class="edit-box">
            <textarea maxlength="50" v-model="editText"></textarea>
            <div class="bottom">
              <div class="left-content">
                <i data-feather="paperclip"></i>
                <i data-feather="smile"></i>
              </div>
              <div class="right-content">
                <button class="cancel" @click="cancel">CANCEL</button>
                <button class="update" @click="updatePost">UPDATE</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="bottom" :class="{'edit-bottom' : editShow}">
      <div class="left-content">
        <div class="like" @click="likePost" :class="{ active: like.active }">
          <i data-feather="thumbs-up"></i>
          <span>{{ like.count }}</span>
        </div>
        <div
          class="dislike"
          @click="dislikePost"
          :class="{ active: dislike.active }"
        >
          <i data-feather="thumbs-down"></i>
          <span>{{ dislike.count }}</span>
        </div>
      </div>
      <div class="right-content">
        <div class="edit" @click="editPost">
          <i data-feather="edit-3"></i>
        </div>
        <div class="trash" @click="trashPost">
          <i data-feather="trash-2"></i>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import feather from "feather-icons";
export default {
  props: ["date", "time", "text", "postList"],
  mounted() {
    feather.replace();
  },
  data() {
    return {
      like: {
        count: 0,
        active: false,
      },
      dislike: {
        count: 9,
        active: false,
      },
      editShow: false,
      editText: "",
    };
  },
  methods: {
    trashPost() {
      let index = this.$vnode.key;

      const postList = this.postList;
      postList.splice(index, 1);

      window.localStorage.setItem("postList", JSON.stringify(postList));
    },
    editPost() {
      this.editShow = true;

      let index = this.$vnode.key;

      this.editText = this.postList[index].text;
    },
    updatePost() {
      let index = this.$vnode.key;

      const postList = this.postList;

      postList[index].text = this.editText;

      window.localStorage.setItem("postList", JSON.stringify(postList));
      this.editShow = false;
    },
    likePost() {
      this.like.active = !this.like.active;
      this.like.active ? this.like.count++ : this.like.count--;
    },
    dislikePost() {
      this.dislike.active = !this.dislike.active;
      this.dislike.active ? this.dislike.count++ : this.dislike.count--;
    },
    cancel() {
      this.editShow = false;
    },
  },
};
</script>
<style>
.content-box {
  box-shadow: 0px 3px 6px #00000029;
  border-radius: 5px;
  background-color: #fff;
  width: 100%;
  margin: 19px 0;
  height: 126px;
  position: relative;
}
.content-box .top-content {
  border-bottom: 1px solid #eaecee;
  padding: 20px 20px 19px;
  display: flex;
  gap: 10px;
  background-color: #fff;
  z-index: 1;
}
.content-box .right-content {
  display: flex;
  align-items: center;
  gap: 10px;
}
.content-box .bottom {
  padding: 13px 20px;
  background-color: #fff;
  z-index: 1;
  border-radius: 0 0 5px 5px;
}
.content-box .content {
  text-align: start;
  width: 100%;
}
.content-box svg {
  margin-right: 0;
}
.edit-box textarea {
  padding-top: 5px;
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
.left-content {
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
.left-content span {
  color: #c1c8ce;
  font-size: 14px;
}
.active svg,
.active span {
  color: #34495e !important;
}
.cancel,
.update {
  padding: 6px 14px !important;
  font-size: 10px !important;
}
.cancel {
  background-color: #fff !important;
  color: #c1c8ce !important;
  box-shadow: none !important;
  padding: 0 !important;
}
.edit-box .bottom {
  padding: 13px 0 0 !important;
}
.edit-box svg {
  margin-right: 13.42px;
}
.edit-bottom {
  box-shadow: 0px 13px 16px #0000005C !important
}
</style>
