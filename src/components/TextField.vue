<template>
  <div >
    <span contenteditable="true" id="editor"  @click="getSelectionText">
        {{textViev}}</span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      textViev: "My lovely little Pony"
    };
  },

  methods: {
    getSelectionText: function() {
      let txt = "";
      if ((txt = window.getSelection)) {
        txt = window.getSelection().toString();
      } else {
        txt = document.selection.createRange().text;
      }
      this.$emit("text", {
        text: txt
      });
    }
  }
};
</script>

<style scoped>
div {
  display: flex;
  max-width: 700px;
  word-wrap: break-word;
}

span {
  text-shadow: rgba(0, 0, 0, 0.2) 2px 2px 0px;
  line-height: 1.5em;
  padding: 10px;
  height: max-content;
  width: max-content;
}

textarea {
  padding: 5px;
  margin-right: 10px;
}
</style>