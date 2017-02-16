<template lang='pug'>
#page-container
  doc-header
  #body-container
    doc-sidebar
    doc-reader
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
<style src='./css/doc_browser.scss' lang='scss'></style>
