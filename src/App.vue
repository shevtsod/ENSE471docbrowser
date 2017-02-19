<template lang='pug'>
#page
  #header: doc-header(v-on:change-state='setState')
  #row
    doc-sidebar
    #content
      //- ADD STATES HERE
      doc-reader(
        v-if=" state.name == 'reader' "
        v-bind:file='file' v-bind:text='text'
        v-on:change-state='setState'
        )
      doc-editor(
        v-if=" state.name == 'editor' "
        v-bind:file='file' v-bind:text='text'
        v-on:change-state='setState'
        v-on:change-text='setText'
        )
    doc-bookmarks
</template>

<script>
import header from './components/Header.vue'
import sidebar from './components/Sidebar.vue'
import reader from './components/Reader.vue'
import bookmarks from './components/Bookmarks.vue'
import editor from './components/Editor.vue'

import placeholder from './placeholder.js'

let STATE = {
  READER: {value: 0, name: 'reader'},
  EDITOR: {value: 1, name: 'editor'},
};


//This is just placeholder text
//In an actual application, we would retrieve data from a database
let defaultText = placeholder;

export default {
  name: 'app',
  components: {
    'doc-header': header,
    'doc-sidebar': sidebar,
    'doc-reader': reader,
    'doc-bookmarks': bookmarks,
    'doc-editor': editor,
  },
  data: function() {
    return {
      state: STATE.READER,

      file: 'Sub-Section 1',
      text: defaultText,
    }
  },
  computed: {
  },
  methods: {
    //Allow children to change the state of the app
    setState(value) {
      switch(value.toLowerCase()) {
        case STATE.READER.name:
          this.state = STATE.READER;
          break;
        case STATE.EDITOR.name:
          this.state = STATE.EDITOR;
          break;
        //ADD NEW STATE CASES HERE
      }
    },
    //Allow children to change the text of the file
    setText(text) {
      this.text = text;
    }
  },
}
</script>


<!-- Global app styles -->
<style lang='scss' src='./css/doc_browser.scss'></style>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<!-- Local styles -->
<style scoped lang='scss'>
@import 'css/doc_browser';

#page {
  display: flex;
  flex-direction: column;

  flex: 1 1 auto;
}

#header {
  flex: 0 0 auto;
}

#row {
  display: flex;

  flex: 1 1 auto;
}

#content {
  @extend .black-border;

  @include css3(border-box, '');
  @include css3(border-bottom, none);

  /* small devices (tablets, 767px and below) */
  @media (max-width: 767px) {
    @include css3(border-right, none);
  }

  flex: 1 1 auto;

  max-height: 100vh;
  max-width: 100vw;

  display: flex;
  flex-direction: row;
  align-items: flex-start;
}
</style>
