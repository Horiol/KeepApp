<template>
  <div id="app">
    <FileManager v-if="fileOpened"
    :file="file"
    :password="password">
    </FileManager>
    <div v-else>
      <input type="file" name="File" id="file"
      @change="processFile($event)">
      <input v-model="password" type="password" name="Password" id="password">
      <button @click="openFile">Open File</button>
    </div>
  </div>
</template>

<script>
import FileManager from "@/components/FileManager";

export default {
  name: "app",
  components: {
    FileManager
  },
  data() {
    return {
      file: null,
      password: null,
      fileOpened: false
    };
  },
  methods: {
    processFile(event) {
      this.file = event.target.files[0];
    },
    openFile: function() {
      if (this.file && this.password) {
        this.fileOpened = true;
      } else {
        alert("File and Password are needed");
      }
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
