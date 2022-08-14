<template>
  <div class="text-box">
    <textarea placeholder="Your text here" maxlength="120" v-model="text"></textarea>
    <div class="bottom">
      <div class="left-content">
        <i data-feather="paperclip"></i>
        <i data-feather="smile"></i>
      </div>
      <div class="right-content">
        <button class="submit" @click="saveText">SUBMIT</button>
      </div>
    </div>
  </div>
</template>
<script>
import feather from 'feather-icons'
import { format } from 'date-fns'

export default {
  mounted(){
    feather.replace();
  },
  props : ["postList"],
  data() {
    return {
      text: ''
    }
  },
  methods: {
    saveText(){
      const date = format(new Date(),"d.MM.yyyy");
      const time = format(new Date(),"h:m");
      
      const post = {
        date : date,
        time : time,
        text : this.text
      }
      
      const postList = this.postList
      postList.push(post)

      window.localStorage.setItem('postList',JSON.stringify(postList));

      this.text = ''
    }
  }
}
</script>
<style>
.text-box {
  box-shadow: 0px 3px 6px #00000029;
  border-radius: 5px;
  background-color: #fff;
  padding: 30px;
  margin-bottom: 19px;
}
textarea {
  resize: none;
  width: 100%;
  border: none;
  height: 72px;
  color: #34495E;
  font-size: 14px;
  transition: all 0.2 ease-out;
}
textarea:focus {
  outline: none !important;
}
textarea::placeholder {
  color: #C1C8CE;  
}
textarea:focus::placeholder {
  color: transparent;
}
.right-content button {
  box-shadow: 0px 3px 6px #8e44ad29;
  border-radius: 5px;
  background-color: #9b59b6;
  color: #fff;
  padding: 10px 25px;
  border: none;
  cursor: pointer;
  letter-spacing: 1.4px;
  font-size: 14px;
  font-weight: 500;
  transition: all 0.2 ease-out;
}
.submit:hover {
  box-shadow: 0px 3px 6px #8e44ad8f;
  background-color: #8e44ad;
}
.bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.bottom svg{
  height: 16px;
  width: auto;
  color: #C1C8CE;
  cursor: pointer;
  margin-right: 13.42px;
}
.bottom svg:hover{
  color: #9b59b6;
}
</style>
