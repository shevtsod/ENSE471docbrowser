<template lang='pug'>
.bookmarks(v-bind:class="displayContent")
  #header
    .chevronlink: a(href='#'): i.chevron.fa(
      v-on:click.prevent='display = !display'
      v-bind:class='displayChevron'
      )
    .title(v-if='display')
      h4 {{ msg }}
  #content(v-if='display')
    div(v-for="bookmark in bookmarks")
      h4 {{ bookmark }}
</template>


<script>
export default {
  name: 'doc-bookmarks',
  data: function() {
    return {
      msg: 'Bookmarks',
      display: false,
      bookmarks: ['Bookmark 1', 'Bookmark 2', 'Bookmark 3'],
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


.hidden-bookmarks {
  flex: 0 0 30px;
}

#header {
  display: flex;
  align-items: center;

  .chevronlink {
    flex: 1 0 auto;
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

  .title {
    flex: 0 0 auto;

    display: flex;
    align-items: flex-end;

    padding-right: 10px;
  }
}

#content {
  flex: 1 1 auto;

  text-align: center;
  margin-top: 10px;

  h4 {
    padding-top: 10px;
    padding-bottom: 10px;
    background-color: $C_BACKGROUND;
    @include css3(border, 1px solid $C_ACCENT);
    @include css3(border-left, none);
    @include css3(border-right, none);

    &:hover {
      cursor: pointer;
      background: $C_ACCENT;
    }
  }
}
</style>
