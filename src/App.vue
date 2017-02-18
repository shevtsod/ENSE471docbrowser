<template lang='pug'>
#page
  #header: doc-header
  #row
    doc-sidebar
    #content: doc-reader
    doc-bookmarks
</template>

<script>
import header from './components/Header.vue'
import sidebar from './components/Sidebar.vue'
import reader from './components/Reader.vue'
import bookmarks from './components/Bookmarks.vue'

export default {
  name: 'app',
  components: {
    'doc-header': header,
    'doc-sidebar': sidebar,
    'doc-reader': reader,
    'doc-bookmarks': bookmarks,
  }
}
</script>


<!-- Global app styles -->
<style lang='scss' src='./css/doc_browser.scss'></style>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<!-- Local styles -->
<style lang='scss' scoped>
@import 'css/doc_browser';

#page {
  display: flex;
  flex-direction: column;

  flex: 1 1 auto;
}

#header {
  flex: 1 1 auto;

  @media (min-width: 768px) {
    flex: 0 1 auto;
  }
}

#row {
  display: flex;

  flex: 1 1 auto;
}

#sidebar {
  display: none;

  /* small devices (tablets, 768px and up) */
  @media (min-width: 768px) {
    display: flex;
    flex: 0 0 270px;
    background-color: $C_DARK_ACCENT;
    border: none;
  }

  overflow-y: auto;
}

#content {
  @extend .black-border;

  @include css3(border-box, '');
  @include css3(border-bottom, none);

  /* small devices (tablets, 767px and below) */
  @media (max-width: 767px) {
    @include css3(border-left, none);
    @include css3(border-right, none);
  }

  overflow: auto;
}
</style>
