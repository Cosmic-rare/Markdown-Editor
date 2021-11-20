<template>
  <div class='content'>
    <div class="tabs">

      <div v-bind:class="{hide: isHide}" class='tabItem'>
        <textarea @input='onChange' v-model='markdown'># Markdown</textarea>
      </div>

      <div v-bind:class="{hide: !isHide}" class='tabItem'>
        <div class='preview markdown-body' v-html='html'></div>
      </div>

    </div>

    <div class='side'>
      <button class='button' @click="toPreview" v-bind:class='{hide: isHide}'><img src='../../public/eye.svg' /></button>
      <button class='button' @click="toEdit" v-bind:class='{hide: !isHide}'><img src='../../public/edit.svg' /></button><br>
      <div class="cont">
        <label class="vote">
          <input type="file" name="image">
          <img src="../../public/image.svg">
        </label>  
      </div>
    </div>

  </div>
</template>

<script>
import md from '../plugins/markdownParser.js';

export default {
  name: 'Home',
  data() {
    return {
      text: '',
      markdown: '# This is Markdown Editor',
      html: '',
      isHide: false,
      imageTemplate: '![](https://upload.wikimedia.org/wikipedia/commons/9/95/Vue.js_Logo_2.svg)'
    }
  },
  methods: {
    onChange() {
      this.html = md.render(this.markdown)
    },
    addImage() {
      this.markdown = this.markdown + `\n${this.imageTemplate}\n`
      this.html = md.render(this.markdown)      
    },
    toEdit() {
      this.isHide = false
    },
    toPreview(){
      this.isHide = true
    }
  },
  mounted: function(){
    this.html = md.render(this.markdown)
  }
}
</script>

<style>
@import "../css/markdown.css";
@import '../css/Home.css';
@import url('https://fonts.googleapis.com/css2?family=Source+Code+Pro&display=swap');

input[type="file"] {
    display: none;
}
</style>