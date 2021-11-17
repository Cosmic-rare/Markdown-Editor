<template>
  <div class="about">
    <h1>This is an about page</h1>
  </div>
  <div class="drop_area" 
    @dragenter="dragEnter" 
    @dragleave="dragLeave" 
    @dragover.prevent 
    @drop.prevent="dropFile" 
    :class="{enter: isEnter}"
  >    
    ファイルアップロード
  </div>
</template>

<script>
export default ({
  data() {
    return {
      isEnter: false,
      file: null
    }
  },
  methods: {
    dragEnter() {
      this.isEnter = true;
    },
    dragLeave() {
      this.isEnter = false;
    },
    dropFile() {
      this.isEnter = false; 
    }
  }
})
</script>

<style>
@import '../css/About.css';
</style>