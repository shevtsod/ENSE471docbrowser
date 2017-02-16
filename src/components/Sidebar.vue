<template lang='pug'>
#sidebar
  #content
    h3 {{ msg }}
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
      msg: 'sidebar',
    }
  },
  computed: {
    upper: function() {
      return this.msg.toUpperCase();
    }
  }
};
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang='scss'>
@import '../css/doc_browser';

#sidebar {
  display: none;

  /* small devices (tablets, 768px and up) */
  @media (min-width: 768px) {
    display: inherit;
    flex: 0 0 200px;   //Defines the width of the sidebar
    background-color: $C_DARK_ACCENT;
    border: none;
  }
}

#content {
  margin-top: 5px;
  margin-left: 10px;
}
</style>
