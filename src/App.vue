<template lang='pug'>
#page
  doc-header
  #row
    doc-sidebar
    #content.ss-container: doc-reader
</template>

<script>
import header from './components/Header.vue'
import sidebar from './components/Sidebar.vue'
import reader from './components/Reader.vue'

export default {
  name: 'app',
  components: {
    'doc-header': header,
    'doc-sidebar': sidebar,
    'doc-reader': reader,
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

#row {
  display: flex;

  flex: 1 1 auto;
}

#content {
  @extend .black-border;

  @include css3(border-box, '');
  @include css3(border-right, none);
  @include css3(border-bottom, none);

  /* small devices (tablets, 768px and up) */
  @media (max-width: 767px) {
    @include css3(border-left, none);
  }

  overflow-y: scroll;
  overflow-x: visible;
}
</style>
