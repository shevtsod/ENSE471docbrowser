<template lang="pug">
#reader
  #content-reader
    #summary
      h1 {{ file }}
      button.btn.btn-primary.edit-button(
          v-on:click.prevent="$emit('change-state', 'editor')"
        )
        |EDIT
    #detail
      p(v-html='preview')
</template>


<script>
import showdown from 'showdown';
//Using showdown for markdown-to-html (see https://github.com/showdownjs/showdown)
let converter = new showdown.Converter();
converter.setOption('headerLevelStart', 2);
converter.setOption('tables', true);
converter.setFlavor('github');

export default {
  name: 'doc-reader',
  props: ['file', 'text'],
  data: function() {
    return {
    }
  },
  computed: {
    preview() {
      //Convert markdown to html using showdown
      return converter.makeHtml(this.text);
    }
  },
  methods: {
    goToEditor() {
      setState('editor');
    }
  },
};
</script>


<style scoped lang="scss">
@import '../css/doc_browser';

#reader {
  display: flex;
  flex-direction: column;
  flex: 1 1 auto;

  min-height: 0;
  max-height: 94vh;
  min-width: 0;
  max-width: 94vw;
  overflow: auto;

  padding: 10px;
}


#content-reader {
  display: flex;
  flex-flow: column;
  align-items: stretch;

  /* small devices (tablets, 768px and up) */
  @media (min-width: 768px) {
    padding-left: 40px;
    padding-right: 10%;
  }

  margin-top: 20px;

  * {
    flex: 1 0 auto;
  }
}

#summary {
  display: flex;
  flex-direction: row;
  @include css3(border-bottom, 2px solid $C_TEXT);

  h1 {
    flex: 1 0 auto;
  }

  .edit-button {
    flex: 0 0 50px;
  }
  padding-bottom: 20px;
  margin-bottom: 10px;
}

#details {
  flex: 1 1 auto;

  display: flex;
  flex-direction: column;
  align-items: stretch;

  min-height: 0;
  max-height: 50vh;
}
</style>
