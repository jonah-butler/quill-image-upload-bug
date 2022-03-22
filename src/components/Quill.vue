<template>
  <div id="editor"></div>
  <button @click="showContents">See Contents</button>
</template>

<script>
import Quill from "quill";

export default {
  name: 'QuillEditor',
  components: {
    Quill
  },
  props: ['label', 'modelValue'],
  data() {
    return {
      quill: undefined,
    };
  },
  mounted() {
    this.quill = new Quill('#editor', {
      placeholder: 'Compose a masterpiece...',
      modules: {
        toolbar: {
          container: [
            [
              'bold',
              'italic',
              'image'
            ],
          ],
          handlers: {
            'image': this.imageHandler
          },
        },
      },
      theme: 'snow',
    });
  },
  methods: {
    imageHandler() {
      // instead of actually saving and returning the image url, i am just using this hard coded image url to simulate what an uploaded image would look like
      const testImg = 'https://files.simplifyingthemarket.com/wp-content/uploads/2022/03/17104811/20220321-KCM-Share-1.jpg';
      // create input ele to call click method and open file browser
      const input = document.createElement('input');
      input.setAttribute('type', 'file');
      input.click();
      input.onchange = () => {
        // upload to server logic goes here
        console.log('uploading image to server');
        // use range index to insert new Delta at correct location
        const range = this.quill.getSelection();
        // insert new url
        const resp = this.quill.insertEmbed(range.index, 'image', testImg);
        // set cursor selection to after the image
        this.quill.setSelection(range.index + 1);
      };
    },
    showContents() {
      console.log(this.quill.root.innerHTML)
    },
  }
}
</script>

<style>
#quill {
  max-width: 550px;
  margin: 0 auto;
}

#quill p img {
  /* margin: 0.25rem 0 0.25rem 0 !important; */
  display: block !important;
  /* max-width: 425px !important;
  max-height: 350px !important; */
}

.ql-toolbar {
  text-align: left;
}

.ql-editor {
  min-height: 100px;
}
input.hidden {
  display: none;
}
</style>