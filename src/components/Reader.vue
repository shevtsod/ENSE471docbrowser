<template lang="pug">
#reader.ss-container
  .space
  p AYY LMAO
</template>


<script>
export default {
  name: 'doc-reader',

  data: function() {
    return {

    }
  },

  computed: {

  },
  methods: {

  },

};
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import '../css/doc_browser';

#reader {
  @extend .black-border;
}

.space {
  height: 2000px;
  width: 1700px;
}
</style>
