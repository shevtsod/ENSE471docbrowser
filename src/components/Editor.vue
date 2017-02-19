<template lang="pug">
#editor
  #summary
    h1 {{ file }}
    button.btn.btn-primary.edit-button(
        v-on:click.prevent="$emit('change-state', 'reader')"
      )
      |EDIT
  #detail
    #input: textarea(v-model='text')
    #output: div(v-html='preview')
    #space
  #control
    |TEST
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
  data: function() {
    return {
      file: 'Sub-Section 1',
      text: '',
    }
  },
  computed: {
    preview() {
      //Convert markdown to html using showdown
      return converter.makeHtml(this.text);
    }
  },
  methods: {
  },
};
</script>


<style scoped lang="scss">
@import '../css/doc_browser';

#editor {
  flex: 1 1 auto;
  align-self: stretch;

  display: flex;
  flex-direction: column;
  align-items: stretch;

  padding: 10px;
}

#summary {
  flex: 0 0 auto;
  display: flex;
  flex-direction: row;

  @include css3(border-bottom, 2px solid $C_TEXT);

  h1 {
    flex: 1 0 auto;
  }

  .edit-button {
    flex: 0 0 auto;
  }

  padding-bottom: 20px;
  margin-bottom: 10px;
}

#detail {
  flex: 1 0 auto;

  display: flex;
  flex-direction: row;
  align-items: stretch;

  /* small devices (tablets, 767px and down) */
  @media (max-width: 767px) {
    flex-direction: column;
  }

  #input {
    align-self: stretch;

    display: flex;
    flex-direction: row;
    align-items: stretch;

    background-color: $C_DARK_ACCENT;

    @include css3(border, 1px solid $C_ACCENT);
    @include css3(border-radius, 5px);

    /* small devices (tablets, 768px and up) */
    @media (min-width: 768px) {
      margin-right: 5px;
      flex: 0 1 50vw;
    }
    @media (max-width: 767px) {
      margin-bottom: 5px;
      flex: 1 1 50vw;
    }
  }

  #output {
    align-self: stretch;

    display: flex;
    flex-direction: column;
    align-items: stretch;

    background-color: $C_DARK_ACCENT;

    color: $C_TEXT;
    background-color: $C_BACKGROUND;

    @include css3(border, 1px solid $C_ACCENT);
    @include css3(border-radius, 5px);

    padding: 10px;

    /* small devices (tablets, 768px and up) */
    @media (min-width: 768px) {
      flex-direction: row;
      flex: 1 1 50vw;
      max-width: 50vw;
      min-width: 0;
    }
    @media (max-width: 767px) {
      flex: 1 1 50vw;
    }

    div {

      max-height: 100%;
      min-height: 0;

      overflow: auto;

      /* small devices (tablets, 768px and up) */
      @media (min-width: 768px) {
        flex: 1 1 80vh;
        white-space: nowrap;
        max-height: 80.5vh;
        min-height: 0;
      }
      @media (max-width: 767px) {
        flex: 1 1 50vw;
      }
    }
  }
}

textarea {
  min-width: 100%;

  resize: none;

  color: $C_TEXT;
  background-color: $C_DARK_ACCENT;

  font-size: 14px;
  padding: 10px;

  @include css3(border, none);
  @include css3(box-shadow, none);
  outline: none;

  overflow: auto;
}

#control {

}
</style>
