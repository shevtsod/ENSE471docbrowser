<template lang="pug">
#editor
  #summary
    h1 {{ file }}
    p Created: Jan. 1, 2017
    p Last Modified: Today
  #detail
    #input: textarea(v-model='textprop')
    #output: div(v-html='preview')
    #space
  #control
    #discard: button.btn.btn-danger.edit-button(
        v-on:click.prevent="$emit('change-state', 'reader')"
      )
      i.fa.fa-times(aria-hidden="true")
      |  DISCARD CHANGES
    #submit: button.btn.btn-success.edit-button(
        v-on:click.prevent="submitChanges"
      )
      i.fa.fa-floppy-o(aria-hidden="true")
      |  SAVE
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
      textprop: this.text,
    }
  },
  computed: {
    preview() {
      //Convert markdown to html using showdown
      return converter.makeHtml(this.textprop);
    }
  },
  methods: {
    submitChanges() {
      //Change the state to the reader
      this.$emit('change-state', 'reader');
      //Pass the new text to the parent
      this.$emit('change-text', this.textprop);
    }
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

  h1 {
    flex: 1 0 auto;
  }

  p {
    flex: 0 1 auto;
    margin-left: 30px;
    align-self: flex-end;
  }

  padding-bottom: 20px;
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

    overflow: auto;

    /* small devices (tablets, 768px and up) */
    @media (min-width: 768px) {
      flex-direction: row;
      flex: 1 1 50vw;
      max-width: 50vw;
      min-width: 0;
      max-height: 77.8vh;
      min-height: 0;
    }
    @media (max-width: 767px) {
      flex: 1 1 50vw;
      max-width: 93vw;
      min-width: 0;
    }

    div {
      /* small devices (tablets, 768px and up) */
      @media (min-width: 768px) {
        flex: 1 1 80vh;
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

  /* small devices (tablets, 768px and up) */
  @media (min-width: 768px) {
    white-space: nowrap;
  }
}

#control {
  background-color: $C_FOREGROUND;
  padding: 10px;
  flex: 0 0 auto;

  display: flex;

  @include css3(border, 1px solid $C_ACCENT);
  @include css3(border-radius, 5px);

  margin-top: 10px;
  #discard {
    flex: 1 1 auto;
  }

  #submit {
    flex: 0 0 auto;
  }
}
</style>
