<template lang="pug"></template>


<script>
export default {
  name: 'window-size',

  data: function() {
    return {
      windowWidth: window.innerWidth,
      smallEdge: true,
    }
  },

  computed: {
    smallDevice () {
      return this.windowWidth < 768 ? true : false;
    }
  },
  methods: {
    setWindowWidth () {
      this.windowWidth = window.innerWidth;
      //Emit event when screen size becomes considered 'small'
      if(this.windowWidth < 768 && this.smallEdge) {
        //Emit a 'small device' custom event
        this.$emit('small-device');
        this.smallEdge = false;
      }
      if(this.windowWidth >= 768) {
        this.smallEdge = true;
      }
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
