<template lang='pug'>
.bookmarks(v-bind:class="displayContent")
  a.chevronlink(href='#'): i.chevron.fa(
    v-on:click='display = !display'
    v-bind:class='displayChevron'
    )
  .content(v-if='display')
    h4 {{ msg }}
</template>


<script>
import WindowSize from './WindowSize.vue'

export default {

  //Compose other components
  mixins: [
    WindowSize,
  ],
  props: {
    windowSize: null,
  },

  name: 'doc-bookmarks',
  data: function() {
    return {
      msg: 'Bookmarks',
      display: false,
    }
  },
  computed: {
    //Hide the bookmarks when display becomes true
    displayContent() {
      return this.display ? '' : 'hidden-bookmarks';
    },
    //Reverse the direction of the chevron when bookmarks are hidden
    displayChevron() {
      return this.display ? 'fa-chevron-left' : 'fa-chevron-right';
    }
  }
};
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang='scss'>
@import '../css/doc_browser';

.bookmarks {
  display: none;

  /* small devices (tablets, 768px and up) */
  @media (min-width: 768px) {
    display: flex;
    flex-direction: column;
    flex: 0 0 270px;
    background-color: $C_DARK_ACCENT;
    border: none;
  }

  @include css3(
    transition,
    all 200ms linear );
}

.content {
  display: flex;
  flex-direction: column;
  flex: 0 0 100%;

  margin-top: 0;
  margin-left: 10px;
}

.chevronlink {
  flex: 0 0 auto;
  align-self: flex-start;
}

a .chevron {
  color: $C_TEXT;
  padding: 10px;

  //Rotation animation transition
  @include css3(
    transition,
    transform 500ms cubic-bezier(0.620, -0.600, 0.260, 1.450) );

  &:hover {
    transform: rotate(180deg);
    cursor: hand;
  }
}

.hidden-bookmarks {
  flex: 0 0 30px;
}
</style>
