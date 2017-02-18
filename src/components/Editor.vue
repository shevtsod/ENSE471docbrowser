<template lang="pug">
#reader
  #content
    #summary
      h1 Sub-Section 1
      button.btn.btn-primary.edit-button(
          v-on:click.prevent="$emit('change-state', 'reader')"
        )
        |EDIT
    #detail
      p
        |Editor
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


<style scoped lang="scss">
@import '../css/doc_browser';

#reader {
  display: flex;
  flex-direction: column;
  flex: 1 0 auto;

  padding: 10px;
}


#content {
  display: flex;
  flex-flow: column;

  /* small devices (tablets, 768px and up) */
  @media (min-width: 768px) {
    padding-right: 10%;
  }

  margin-top: 20px;

  * {
    flex: 1 0 auto;
    margin-bottom: 20px;
  }
}

#summary {
  display: flex;
  flex-direction: row;

  h1 {
    flex: 1 0 auto;
  }

  .edit-button {
    flex: 0 0 50px;
    align-self: flex end;
  }
}
</style>
