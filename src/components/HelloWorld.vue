<script>

import '@toast-ui/editor/dist/toastui-editor.css'
import { Editor } from '@toast-ui/vue-editor';
import axios from 'axios';


export default {
    components: {
      editor: Editor
    },
    data() {
      return {
        editorText: 'TEXT',
        editorOptions: {
          hideModeSwitch: true
        }
      };
    },
    methods: {
      getHTML() {
        this.editorText = this.$refs.toastuiEditor.invoke('getHTML');
      },
      savePDF() {
        axios.post('http://127.0.0.1:8000/api/pdf-saver', {
            editorVal: this.editorText
          })
          .then(function (response) {
            console.log(response);
          })
          .catch(function (error) {
            console.log(error);
          });
      }
    }
}
</script>

<template>
  <div>
    <h2> VALUE => {{ editorText }}</h2>
    <editor ref="toastuiEditor" @change="() => getHTML()" />
    <button @click="() => savePDF()">
      To PDF
    </button>
  </div>
</template> 

<style>
h2 {
  color: black;
}
</style>