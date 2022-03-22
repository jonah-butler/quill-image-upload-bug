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
              'underline',
              'strike',
              {'font': [] },
              {'align': [] },
              'image'
            ],
            [
              'blockquote',
              'link',
              { 'header': [1,2,3] },
              { 'list': 'ordered' },
              { 'list': 'bullet' },
              { 'size': ['small', false, 'large', 'huge'] }
            ],
            [
              { 'color': [] },
              { 'background': [] }
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
      console.log('image handler event fired');
      const input = document.createElement('input');
      const testImg = 'https://files.simplifyingthemarket.com/wp-content/uploads/2022/03/17104811/20220321-KCM-Share-1.jpg';
      input.setAttribute('type', 'file');
      input.click();
      input.onchange = () => {
        const file = input.files[0];
        // file type is only image.
        if (/^image\//.test(file.type)) {
          console.log('uploading image to server');
          const range = this.quill.getSelection();
          const resp = this.quill.insertEmbed(range.index, 'image', testImg);
          this.quill.setSelection(range.index + 1);
        } else {
          console.warn('You could only upload images.');
        }
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