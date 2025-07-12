<template>
  <div class="container mt-5">
    <CCard
        class="shadow border" :style="{ borderRadius: '20px', boxShadow: '0 8px 20px rgba(0, 0, 0, 0.15)', transition: 'box-shadow 0.3s ease' }">
      <CCardBody>
        <div class="text-center mb-4 mt-4">
          <h4 class="fw-bold">President of the Student Union Candidate Register</h4>
          <p class="mb-1">Upload JPG Image</p>
          <small class="text-danger fw-semibold">*1080x1080 px</small>
        </div>

        <CForm>
          <CRow class="align-items-center mb-4">
            <CCol md="9">
              <input type="text" class="form-control" placeholder="Profile Image File" :value="profileFileName" disabled/>
            </CCol>
            <CCol md="3">
              <input type="file" ref="profileInput" class="d-none" accept="image/jpeg,image/png" @change="handleProfileSelect"/>
              <button type="button" class="btn btn-outline-primary w-100" @click="triggerProfileUpload">
                Choose File
              </button>
            </CCol>
          </CRow>
          <CRow class="mb-4">
            <CCol md="6" class="mb-3">
              <input type="text" class="form-control" :class="{ 'is-invalid': errors.name }" placeholder="Name" v-model="form.name"/>
              <div class="invalid-feedback" v-if="errors.name">{{ errors.name }}</div>
            </CCol>
            <CCol md="6" class="mb-3">
              <input type="text" class="form-control" :class="{ 'is-invalid': errors.studentID }" placeholder="Student ID" v-model="form.studentID"/>
              <div class="invalid-feedback" v-if="errors.studentID">{{ errors.studentID }}</div>
            </CCol>
            <CCol md="6" class="mb-3">
              <input type="text" class="form-control" :class="{ 'is-invalid': errors.school }" placeholder="School" v-model="form.school"/>
              <div class="invalid-feedback" v-if="errors.school">{{ errors.school }}</div>
            </CCol>
            <CCol md="6" class="mb-3">
              <input type="text" class="form-control" :class="{ 'is-invalid': errors.major }" placeholder="Major" v-model="form.major"/>
              <div class="invalid-feedback" v-if="errors.major">{{ errors.major }}</div>
            </CCol>
            <CCol md="6" class="mb-3">
              <input type="text" class="form-control" :class="{ 'is-invalid': errors.lineID }" placeholder="Line ID" v-model="form.lineID"/>
              <div class="invalid-feedback" v-if="errors.lineID">{{ errors.lineID }}</div>
            </CCol>

            <CCol md="6" class="mb-3">
              <select class="form-control" :class="{ 'is-invalid': errors.gpaLevel }" v-model="form.gpaLevel">
                <option disabled value="">Select GPA Level</option>
                <option>High school transcript(1st year only)</option>
                <option>Bachelor transcript</option>
              </select>
              <div class="invalid-feedback" v-if="errors.gpaLevel">{{ errors.gpaLevel }}</div>
            </CCol>

            <CCol md="6" class="mb-3">
              <input type="text" class="form-control" :class="{ 'is-invalid': errors.gpax }" placeholder="GPAX" v-model="form.gpax"/>
              <div class="invalid-feedback" v-if="errors.gpax">{{ errors.gpax }}</div>
            </CCol>

            <CCol md="6">
              <CRow class="align-items-center">
                <CCol md="8">
                  <input type="text" class="form-control" placeholder="Transcript File" :value="transcriptFileName" disabled/>
                </CCol>
                <CCol md="4">
                  <input type="file" ref="transcriptInput" class="d-none" accept="image/jpeg,image/png" @change="handleTranscriptSelect"/>
                  <button type="button" class="btn btn-outline-primary w-100" @click="triggerTranscriptUpload">
                    Choose File
                  </button>
                </CCol>
              </CRow>
            </CCol>
          </CRow>

          <!-- Policy -->
          <CCardHeader class="fw-bold fs-5 mt-4">
            <h4>Write your policy here</h4>
          </CCardHeader>
          <CCardBody>
            <quill-editor v-model="form.policy" :options="editorOptions" :class="{ 'is-invalid': errors.policy }" style="min-height: 200px"/>
            <div class="text-danger mt-1" v-if="errors.policy">{{ errors.policy }}</div>
          </CCardBody>

          <!-- Submit Button -->
          <div class="text-center mb-4">
            <CButton color="danger" size="lg" shape="pill" @click="submitForm">Submit</CButton>
          </div>
        </CForm>
      </CCardBody>
    </CCard>

    <!-- Toaster -->
    <CToaster position="top-center">
      <CToast
          v-for="(toast, index) in toasts"
          :key="index"
          :show="true"
          :autohide="toast.autohide"
          :header="toast.header"
          :close-button="toast.closeButton"
          :class="toast.class"
          @close="removeToast(index)"
      >
        {{ toast.body }}
      </CToast>
    </CToaster>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import Vue from 'vue'
import VueQuillEditor from 'vue-quill-editor'
import 'quill/dist/quill.core.css'
import 'quill/dist/quill.snow.css'
import 'quill/dist/quill.bubble.css'

import { CToaster, CToast } from '@coreui/vue'

Vue.use(VueQuillEditor)

export default {
  name: 'registerPage',
  components: {
    CToaster,
    CToast
  },
  props: {
    icon: {
      type: String,
      default: 'cil-bell'
    },
    caption: {
      type: String,
      default: 'ศูนย์แจ้งเหตุฉุกเฉิน'
    }
  },
  data() {
    return {
      profileFileName: '',
      transcriptFileName: '',
      form: {
        name: '',
        studentID: '',
        school: '',
        major: '',
        lineID: '',
        gpaLevel: '',
        gpax: '',
        policy: ''
      },
      errors: {},
      editorOptions: {
        placeholder: 'Type your policy here...',
        theme: 'snow'
      },
      toasts: []
    }
  },
  methods: {
    onInit() {},

    triggerProfileUpload() {
      this.$refs.profileInput.click()
    },
    triggerTranscriptUpload() {
      this.$refs.transcriptInput.click()
    },
    handleProfileSelect(event) {
      const file = event.target.files[0]
      this.profileFileName = file ? file.name : ''
    },
    handleTranscriptSelect(event) {
      const file = event.target.files[0]
      this.transcriptFileName = file ? file.name : ''
    },
    submitForm() {
      this.errors = {}
      if (this.isFormValid()) {
        this.toasts.push({
          header: 'Success',
          body: 'Form submitted successfully!',
          autohide: 3000,
          closeButton: true,
          class: 'toast-soft-green'
        })
      } else {
        this.toasts.push({
          header: 'Error',
          body: 'Please fill in all required fields.',
          autohide: 3000,
          closeButton: true,
          color: 'danger'
        })
      }
    },
    isFormValid() {
      const requiredFields = ['name', 'studentID', 'school', 'major', 'lineID', 'gpaLevel', 'gpax', 'policy']
      let valid = true
      requiredFields.forEach(field => {
        if (!this.form[field]) {
          this.errors[field] = 'This field is required'
          valid = false
        }
      })
      return valid
    },
    removeToast(index) {
      this.toasts.splice(index, 1)
    }
  },
  computed: {
    ...mapGetters({})
  }
}
</script>

<style scoped>
.is-invalid {
  border: 1px solid #dc3545 !important;
  border-radius: 0.375rem;
}
.toast-soft-green .toast-header {
  background-color: #e7f7ec !important;
  color: #2e7d32 !important;
}
.toast-soft-green .toast-body {
  background-color: #f2fdf6 !important;
  color: #2e7d32 !important;
}
</style>
