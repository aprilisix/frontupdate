<template>
  <div class="condition-wrapper text-center py-5">
    <h4 class="condition-title mb-4">{{ headerText }}</h4>

    <CRow class="justify-content-center">
      <CCol cols="12" md="8">
        <img :src="conditionImage" class="condition-image" alt="Condition Banner" />
      </CCol>
    </CRow>

    <CRow class="justify-content-center mt-4">
      <CCol cols="auto">
        <button class="btn-submit px-5 py-2" @click="onSubmit">
          Submit
        </button>
      </CCol>
    </CRow>
  </div>
</template>

<script>
import conditionBanner from '@/assets/banner/condition2.jpg'

export default {
  name: 'condition_normal',
  data() {
    return {
      headerText: 'Please Read the Following Conditions',
      conditionImage: conditionBanner,
    }
  },
  methods: {
    onSubmit() {
      this.$router.push('/register/register_normal')
    }
  }
}
</script>

<style scoped>
.condition-wrapper {
  font-family: 'Mitr', sans-serif;
  background-color: #f9f9f9;
  min-height: 100vh;
}

.condition-title {
  font-size: 1.5rem; /* ← ปรับตรงนี้ */
  font-weight: bold;
  color: #333;
  margin-bottom: 1.5rem;
}

.condition-image {
  width: 100%;
  max-width: 600px;
  height: auto;
  margin: 0 auto;
  display: block;
  border-radius: 12px;
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.1);
  object-fit: contain;
}

.btn-submit {
  background-color: #C39434;
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 1rem;
  transition: background-color 0.3s ease;
}

.btn-submit:hover {
  background-color: #a67c2b;
  cursor: pointer;
}
</style>

