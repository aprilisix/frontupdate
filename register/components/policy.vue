<template>
  <CCard>
    <CCardHeader>
      Write your policy here
      <a
          href="https://coreui.io/pro/vue/"
          rel="noreferrer noopener"
          target="_blank"
          class="badge badge-danger ml-1"
      >
        CoreUI Pro
      </a>
      <div class="card-header-actions">
        <a
            href="https://github.com/surmon-china/vue-quill-editor"
            rel="noreferrer noopener"
            target="_blank"
            class="card-header-action"
        >
          <small class="text-muted">docs</small>
        </a>
      </div>
    </CCardHeader>
    <CCardBody>
      <quill-editor :content="content"/>
    </CCardBody>
  </CCard>
</template>

<script>
import Vue from 'vue'
import VueQuillEditor from 'vue-quill-editor'
import 'quill/dist/quill.core.css'
import 'quill/dist/quill.snow.css'
import 'quill/dist/quill.bubble.css'

Vue.use(VueQuillEditor)

export default {
  name: 'text-editors',
  data () {
    return {
      content: `<p></p>`
    }
  }
}
</script>
