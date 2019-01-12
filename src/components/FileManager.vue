<template>
    <div>
        File: {{file.name}}
    </div>
</template>

<script>
import kdbxweb from "kdbxweb";

export default {
  name: "FileManager",
  props: ["file", "password"],
  data() {
    return {
      fileData: null
    };
  },
  mounted: function() {
    var fileReader = new FileReader();
    const th = this;
    fileReader.onload = function(event) {
      th.fileData = event.target.result;
      th.OpenFile();
    };
    fileReader.readAsArrayBuffer(this.file);
  },
  methods: {
    OpenFile: function() {
      var credentials = new kdbxweb.Credentials(
        kdbxweb.ProtectedValue.fromString(this.password),
        this.fileData
      );
      kdbxweb.Kdbx.load(this.fileData, credentials).then(db => {
        console.log(db);
      });
    }
  }
};
</script>
