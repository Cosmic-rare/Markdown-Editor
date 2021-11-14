<template>
  <div class='main'>
    <div class='editor'>
      <textarea @input='onChange' v-model='markdown'># Markdown</textarea>
    </div>
    <div class='preview' v-html='html'>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data() {
    return {
      text: '',
      markdown: '<h1>Hello!</h1>\na\n<p>Oh! This is HTML Editor!</p>\n<style>\nh1{font-size:100px;color:#1f1;margin:0px;}\n</style>',
      html: ''
    }
  },
  methods: {
    onChange() {
      this.html = this.markdown
    }
  },
  mounted: function(){
    this.html = this.markdown
  }
}
</script>

<style>
textarea {
  width: 200px;
  height: 300px;
}

.preview {
  width: 200px;
  height: 300px;
  background-color: #999;
}
</style>