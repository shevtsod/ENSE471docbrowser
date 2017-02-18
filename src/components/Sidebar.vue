<template lang='pug'>
.sidebar(v-bind:class="{ 'min-sidebar': displayContent }")
  #header
    .title
      h4 {{ msg }}
    a.chevronlink(href='#'): i.chevron.fa(
      v-on:click='minimize = !minimize'
      v-bind:class='reverseChevron'
      )
  #content
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

  name: 'doc-sidebar',
  data: function() {
    return {
      msg: 'Sidebar',
      minimize: false,
    }
  },
  computed: {
    //Minimize the bookmarks when minimize is true
    displayContent() {
      return (this.minimize || this.smallDevice)
          ? true
          : false;
    },
    //Reverse the direction of the chevron when bookmarks are hidden
    reverseChevron() {
      return (this.minimize || this.smallDevice)
          ? 'fa-chevron-right'
          : 'fa-chevron-left';
    }
  }
};
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang='scss'>
@import '../css/doc_browser';

.sidebar {
  display: flex;
  flex-direction: column;
  flex: 0 0 270px;
  background-color: $C_DARK_ACCENT;
  border: none;


  @include css3(
    transition,
    all 200ms linear );
}


.min-sidebar {
  flex: 0 0 30px;
}

#header {
  display: flex;
  align-items: center;

  .chevronlink {
    flex: 0 0 auto;
  }

  .title {
    flex: 1 0 auto;
    padding-left: 10px;
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
}
</style>
