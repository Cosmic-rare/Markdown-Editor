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

textarea {
  margin: 0px;
  width: 100%;
  height: 500px;
}

/*タブ切り替え全体のスタイル*/
.tabs {
  margin-top: 50px;
  padding-bottom: 40px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
  width: 80%;
  max-width: 800px;
  margin: 0 auto;
}

/*タブのスタイル*/
.tab_item {
  width: calc(100%/2);
  height: 50px;
  border-bottom: 3px solid #5ab4bd;
  background-color: #d9d9d9;
  line-height: 50px;
  font-size: 16px;
  text-align: center;
  color: #565656;
  display: block;
  float: left;
  text-align: center;
  font-weight: bold;
  transition: all 0.2s ease;
}
.tab_item:hover {
  opacity: 0.75;
}

/*ラジオボタンを全て消す*/
input[name="tab_item"] {
  display: none;
}

/*タブ切り替えの中身のスタイル*/
.tab_content {
  display: none;
  padding: 40px 40px 0;
  clear: both;
  overflow: hidden;
}


/*選択されているタブのコンテンツのみを表示*/
#edit:checked ~ #edit_content,
#preview:checked ~ #preview_content {
  display: block;
}

/*選択されているタブのスタイルを変える*/
.tabs input:checked + .tab_item {
  background-color: #5ab4bd;
  color: #fff;
}
</style>