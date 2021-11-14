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
.drop_area {
  color: gray;
  font-weight: bold;
  font-size: 1.2em;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 500px;
  height: 300px;
  border: 5px solid gray;
  border-radius: 15px;
}

.enter {
    border: 10px dotted powderblue;
}
</style>