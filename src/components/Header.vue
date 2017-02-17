<template lang="pug">
nav.navbar.navbar-inverse.navbar-static-top
  .container-fluid
    .navbar-header
      a.navbar-brand(
        href='#'
        v-on:mouseenter='icon = !icon'
        v-on:mouseleave='icon = !icon'
      )
        i(v-bind:class='getIcon')
        //img(alt='brand' src='../assets/logo.png')
        span {{ headerTitle }}
      button.navbar-toggle.collapsed(
          type='button'
          data-toggle='collapse'
          data-target='#navbar-to-collapse'
        )
        span.sr-only Toggle navigation
        span.icon-bar
        span.icon-bar
        span.icon-bar
    #navbar-to-collapse.collapse.navbar-collapse
      .navbar-form.navbar-right
        .input-group.form-group
          input.form-control(type='text' placeholder='Search')
          span.input-group-btn
            button.btn.btn-default(href='#')
              span.glyphicon.glyphicon-search
      .nav.navbar-right
        ul.nav.navbar-nav.navbar-right
          li: a(href='#') Link 1
          li: a(href='#') Link 2
</template>


<script>
import WindowSize from './WindowSize.vue'

export default {
  name: 'doc-header',

  //Compose other components
  mixins: [
    WindowSize,
  ],
  props: {
    windowSize: null,
  },

  data: function() {
    return {
      icon: false,
    }
  },

  computed: {
    // If icon is an image
    /*
    logo () {
      // This is the required method of specifying an image path with webpack
      // in JavaScript
      return require('../assets/' + this.id + '.png');
    },
    */
    // If icon is a font-awesome icon
    getIcon () {
      return this.icon ? 'fa fa-bookmark fa-lg' : 'fa fa-bookmark-o fa-lg'
    },
    // Header title depends on size of display (on tablets and smaller, just
    // display an acronym)
    headerTitle() {
      return this.windowWidth < 768
        ? 'DB'
        : 'Documentation Browser';
    }
  },
};
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import '../css/doc_browser';

.navbar {
  margin: 0;
  border: none;
}

//brand section
.navbar-brand {
  display: inline;

  //logo
  img, i {
    display: inline-block;

    //Rotation animation transition
    @include css3(
        transition,
        transform 600ms cubic-bezier(0.620, -0.600, 0.260, 1.850) );
  }

  //'headertitle'
  span {
    margin-left: 15px;
  }

  &:hover {
    span {
      font-weight:bolder;
    }

    i {
      //Rotation animation effect
      transform: rotate(90deg);
    }
  }
}

//search bar
.form-control {
  /* small devices (tablets, 768px and up) */
  @media (min-width: 768px) {
    margin-left: 40px;
  }
}
</style>
