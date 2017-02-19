<template lang='pug'>
.sidebar(v-bind:class="{'min-sidebar': displayContent }")
  #header
    .title(v-if='!minimize')
      h4 {{ msg }}
    a.chevronlink(href='#'): i.chevron.fa(
      v-on:click.prevent='minimize = !minimize'
      v-bind:class='reverseChevron'
      )
  #content(v-if='!minimize')
    .project(v-for="(project, index) in projects")
      i.fa.fa-caret-down
      h5 Project {{ index + 1 }}
      .subsection(v-for="subsection in project")
        i.fa.fa-circle
        h6 {{ subsection }}
</template>


<script>
import WindowSize from './WindowSize.vue'

//Placeholder projects
//In an actual application, we would retrieve data from a database
let project1 = ['Sub-Section 1', 'Sub-Section 2', 'Sub-Section 3'];
let project2 = ['Sub-Section 1'];
let project3 = ['Sub-Section 1', 'Sub-Section 2'];
let projects = [project1, project2, project3];

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
      projects: projects,
    }
  },
  computed: {
    //Minimize the bookmarks when minimize is true
    displayContent() {
      return (this.minimize)
          ? true
          : false;
    },
    //Reverse the direction of the chevron when bookmarks are hidden
    reverseChevron() {
      return (this.minimize)
          ? 'fa-chevron-left'
          : 'fa-chevron-right';
    }
  },

  //Listen to window resize events
  mounted() {
    //Get initial size
    if(this.smallDevice) {
      this.minimize = true;
    }

    //Listen to 'small-device' event from WindowSize
    this.$on('small-device', function () {
      this.minimize = true;
    });
  },
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

#content {
  margin-top: 5px;
  margin-left: 25px;
  h5, h6 {
    display: inline-block;
    padding-left: 10px;
  }

  .project {
    &:hover {
      cursor: pointer;

      h5, .fa-caret-down {
        color: white;
      }
    }
  }

  .subsection {
    margin-left: 20px;
    padding-top: 10px;
    padding-bottom: 10px;

    &:hover {
      cursor: pointer;
      color: white;
    }
  }
}
</style>
