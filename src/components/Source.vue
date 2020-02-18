<template>
  <div id="app">
    <div>
      <div>
        <input
          type="file"
          class="hidden"
          ref="uploadImgInput"
          @change="updateCurrImg($event)"
          accept="image/*"
        />
      </div>
      <div>
        <button @click="updateGeneral()">Pressione</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      avatarUrl: ""
    };
  },
  methods: {
    updateCurrImg(event) {
      this.avatarUrl = event.target.files[0];
    },
    updateGeneral() {
      let fd = new FormData();
      fd.append("image", this.avatarUrl);
      fd.append("name", "name");
      fd.append("surname", "surname");
      fd.append("phoneNumber", "1836962585");
      fd.append("gender", "male");

      var myInit = {
        method:
          "PUT" /*
        headers: {
          "Content-Type": "multipart/form-data"
        },*/,
        mode: "cors",
        cache: "default",
        body: fd
      };
      fetch("http://localhost:62941/api/source/update-general", myInit)
        .then(c => c.json())
        .then(c => alert(c));
    }
  }
};
</script>

<style>
</style>
