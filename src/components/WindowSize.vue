<template lang="pug"></template>


<script>
export default {
  name: 'window-size',

  data: function() {
    return {
      windowWidth: document.documentElement.clientWidth,
    }
  },

  computed: {
    smallDevice () {
      this.$emit('smallDevice');
      return this.windowWidth < 768 ? true : false;
    }
  },
  methods: {
    setWindowWidth () {
      this.windowWidth = document.documentElement.clientWidth;
    },
  },

  //Attach browser resize listeners
  mounted() {
    window.addEventListener('resize', this.setWindowWidth);
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.setWindowWidth);
  },
};
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss"></style>
