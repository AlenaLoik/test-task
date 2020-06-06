<template>
  <div>
    <section>
      <label>
        fonth color:
        <input @change="changeBgColor" value="bgColor" type="color" name="color" />
      </label>
      <label>
        text color:
        <input @change="changeTextColor" value="textColor" type="color" name="color" />
      </label>
      <label>
        font-size
        <select @change="changeFontSize" v-model="fontSize">
          <option v-for="option in options" v-bind:key="option" v-bind:value="option">{{ option }}</option>
        </select>
      </label>
    </section>
    <TextField @text="onText" />
  </div>
</template>

<script>
import TextField from "@/components/TextField";

export default {
  data() {
    return {
      textColor: "textColor",
      fontSize: "12px",
      bgColor: "#ffffff",
      options: ["8px", "12px", "16px", "20px", "24px", "30px", "40px"],
      textForEdit: "",
      textArry: [],
    };
  },
  methods: {
    changeTextColor(event) {
      this.textColor = event.target.value;
      const editParams = "TC";
      this.handleEditing(this.textForEdit, editParams);
    },

    changeFontSize(event) {
      this.fontSize = event.target.value;
      const editParams = "FS";
      this.handleEditing(this.textForEdit, editParams);
    },

    changeBgColor(event) {
      this.bgColor = event.target.value;
      const editParams = "BC";
      this.handleEditing(this.textForEdit, editParams);
    },

    handleEditing(text, editParams) {
      const root = document.getElementById("editor").firstChild;
      const textNode = document.getElementById("editor").firstChild;
      if (textNode) {
        this.textArry.push(textNode.nodeValue);
      }
      
      const content = root.nodeValue;

      console.log(this.textArry)

      if (~content.indexOf(text)) {
        if (document.createRange) {
          const rng = document.createRange();
          rng.setStart(root, content.indexOf(text));
          rng.setEnd(root, content.indexOf(text) + text.length);
          const highlightDiv = document.createElement("span");
          switch (editParams) {
            case "TC":
              highlightDiv.style.color = this.textColor;
              break;
            case "FS":
              highlightDiv.style.fontSize = this.fontSize;
              break;
            case "BC":
              highlightDiv.style.backgroundColor = this.bgColor;
              break;
              default:
                alert('try agane')
          }
          rng.surroundContents(highlightDiv);
        } else {
          alert("Sorry, but you have IE8-, editor is not working...");
        }
      } else {
        alert("error");
      }
    },

    onText({ text }) {
      this.textForEdit = text;
    }
  },
  components: {
    TextField
  }
};
</script>

<style scoped>
section {
  display: flex;
  align-items: center;
  background-color: rgba(65, 105, 225, 0.397);
  margin-bottom: 20px;
}
label {
  display: flex;
  flex-direction: column;
  justify-content: center;
  max-width: 200px;
  align-items: center;
  margin: 15px 60px;
  text-transform: uppercase;
  font-weight: bold;
}
</style>