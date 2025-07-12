<template>
  <div class="pdpa-wrapper text-center py-5">
    <h3 class="pdpa-title mb-4">{{ headerText }}</h3>

    <CRow class="justify-content-center">
      <CCol cols="12" md="8">
        <img :src="pdpaImage" class="img-fluid rounded shadow" alt="PDPA Banner" />
      </CCol>
    </CRow>

    <CRow class="justify-content-center mt-4">
      <CCol cols="12" md="8" class="d-flex justify-content-center align-items-center">
        <label class="custom-radio-label d-flex align-items-center">
          <input
              type="checkbox"
              class="custom-radio-input"
              v-model="agreeChecked"
              @change="onCheckboxChange"
          />
          <span class="custom-radio-check me-3"></span>
          <span class="radio-text">{{ radioLabel }}</span>
        </label>
      </CCol>
    </CRow>

    <CRow class="justify-content-center mt-4" v-if="showSubmit">
      <CCol cols="auto">
        <button
            :disabled="!agreeChecked"
            :class="['submit-btn btn px-5 py-2', agreeChecked ? 'active' : '']"
            id="submitBtn"
            @click="onSubmit"
        >
          Submit
        </button>
      </CCol>
    </CRow>
  </div>
</template>

<script>
import Swal from 'sweetalert2'
import pdpaBanner from '@/assets/banner/PDPA.jpg'

export default {
  name: 'PdpaConsent',

  data() {
    return {
      headerText: 'PDPA',
      radioLabel: 'I agree to Permission to collect personal data',
      pdpaImage: pdpaBanner,
      swalMessage: 'By checking this box, you agree to the terms regarding personal data collection.',
      agreeChecked: false,
      showSubmit: false,
      pdpaKey: 'pdpa_president',
      checkboxKey: 'pdpa_checkbox_state_president',
    }
  },

  mounted() {
    this.updateKeysFromType();
    this.restoreCheckboxState();
  },

  methods: {
    updateKeysFromType() {
      const type = this.$route.params.type;
      this.pdpaKey = `pdpa_${type}`;
      this.checkboxKey = `pdpa_checkbox_state_${type}`;
    },

    restoreCheckboxState() {
      const isChecked = localStorage.getItem(this.checkboxKey) === 'true';
      this.agreeChecked = isChecked;
      this.showSubmit = isChecked;
    },

    onCheckboxChange() {
      localStorage.setItem(this.checkboxKey, this.agreeChecked.toString());

      if (this.agreeChecked) {
        Swal.fire({
          text: this.swalMessage,
          confirmButtonText: 'OK',
        }).then(() => {
          this.showSubmit = true;
        });
      } else {
        this.showSubmit = false;
      }
    },

    onSubmit() {
      if (this.agreeChecked) {
        localStorage.setItem(this.pdpaKey, 'true');
        localStorage.removeItem(this.checkboxKey);

        const type = this.$route.params.type;
        if (type === 'president') {
          this.$router.push('/condition/condition_union');
        } else if (type === 'school') {
          this.$router.push('/condition/condition_school');
        } else if (type === 'normal') {
          this.$router.push('/condition/condition_normal');
        } else {
          this.$router.push('/');
        }
      }
    },
  },
}
</script>

<style scoped>
.pdpa-wrapper {
  font-family: 'Mitr', sans-serif;
  background-color: #f9f9f9;
  min-height: 100vh;
}

.pdpa-title {
  font-size: 2.5rem;
  font-weight: bold;
  color: #333;
}

.radio-text {
  font-size: 1.2rem;
  color: #333;
}

.custom-radio-label {
  cursor: pointer;
}

.custom-radio-input {
  display: none;
}

.custom-radio-check {
  width: 24px;
  height: 24px;
  border: 2px solid #C39434;
  border-radius: 50%;
  position: relative;
}

.custom-radio-input:checked + .custom-radio-check::after {
  content: '';
  position: absolute;
  top: 4px;
  left: 4px;
  width: 12px;
  height: 12px;
  background-color: #C39434;
  border-radius: 50%;
}

.submit-btn {
  background-color: gray;
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 1rem;
  cursor: not-allowed;
  transition: background-color 0.3s ease;
}

.submit-btn.active {
  background-color: #C39434;
  cursor: pointer;
}

.submit-btn.active:hover {
  background-color: #a67c2b;
}
</style>
