<template>
  <div class='main'>
    <div class="tabs">
      <input id="edit" type="radio" name="tab_item" checked>
      <label class="tab_item" for="edit">EDIT</label>
      <input id="preview" type="radio" name="tab_item">
      <label class="tab_item" for="preview">PREVIEW</label>

  <div class="tab_content" id="edit_content">
    <div class="tab_content_description">
          <div class='editor'>
      <textarea @input='onChange' v-model='markdown'># Markdown</textarea>
    </div>
    </div>
  </div>
  <div class="tab_content" id="preview_content">
    <div class="tab_content_description">
         <div class='preview markdown-body' v-html='html'>
    </div>
    </div>
  </div>
</div>

 
  </div>
</template>

<script>
const hljs = require('highlight.js')

const md = require('markdown-it')({
  langPrefix:'hljs language-',
  highlight: function (str, lang) {
    if (lang && hljs.getLanguage(lang)) {
      try {
        return hljs.highlight(str, { language: lang }).value;
      } catch (__) {console.error('MarkdownParse Error')}
    }
    return '';
  }
})

export default {
  name: 'Home',
  data() {
    return {
      text: '',
      markdown: '# This is Markdown Editor',
      html: ''
    }
  },
  methods: {
    onChange() {
      this.html = md.render(this.markdown)
    }
  },
  mounted: function(){
    this.html = md.render(this.markdown)
  }
}
</script>

<style>
@import "../css/preview.css";
@import '../css/home_tabs.css';

textarea {
  margin: 0px;
  width: 100%;
  height: 500px;
}

</style>