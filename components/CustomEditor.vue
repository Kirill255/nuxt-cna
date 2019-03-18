<template>
  <div>
    <div class="field">
      <div class="control">
        <medium-editor class="textarea" :text='aboutText' :options='options' custom-tag='div' v-on:edit='applyTextEdit'></medium-editor>
      </div>
    </div>
  </div>
</template>

<script>
import MediumEditor from "vue2-medium-editor";
import "medium-editor/dist/css/medium-editor.min.css";
import "medium-editor/dist/css/themes/roman.min.css";

export default {
  name: "CustomEditor",
  components: { MediumEditor },
  model: {
    prop: "aboutText"
  },
  props: {
    aboutText: {
      type: String,
      default: ""
    }
  },
  data() {
    return {
      // editor: null,
      options: {
        toolbar: {
          buttons: [
            "bold",
            "italic",
            "h1",
            "h2",
            "h3",
            "anchor",
            "quote",
            "pre",
            "orderedlist",
            "unorderedlist",
            "indent",
            "outdent",
            "justifyLeft",
            "justifyCenter",
            "justifyRight",
            "removeFormat"
          ],
          diffLeft: 80,
          diffTop: -20
        },
        // buttonLabels: "fontawesome",
        disableDoubleReturn: true,
        disableExtraSpaces: true,
        targetBlank: true,
        placeholder: {
          text: "Напишите о себе",
          hideOnClick: false
        },
        paste: {
          forcePlainText: false,
          cleanPastedHTML: true
        }
      }
    };
  },
  methods: {
    applyTextEdit(operation) {
      // console.log("operation :", operation);
      this.$emit("input", operation.api.origElements.innerHTML);
      // or
      // this.$emit("input", operation.event.target.innerHTML);
    }
  }
};
</script>

<style scoped>
</style>

<!-- вроде должны были сделать в 1.1.6 версии поддержку SSR, я попробовал, но не работает -->