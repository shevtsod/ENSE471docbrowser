<template lang='pug'>
#page-container
  doc-header
  #body-container
    doc-sidebar
    doc-reader#content-container
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
<style lang='scss'>
@import 'css/doc_browser';

#page-container {
  display: flex;
  min-height: 100vh;
  flex-direction: column;
  overflow: hidden;
}

#body-container {
  display: flex;
  flex: 1;
  overflow: hidden;
}

#content-container {
 display: flex;
 flex: 1;
 flex-direction: column;
 overflow-y: scroll;
 overflow-x: visible;
}
</style>
