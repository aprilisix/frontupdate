<template>
  <div class="container py-5">
    <h3 class="text-center mb-4">
      President of the Student Assosiation Result
    </h3>

    <CRow id="candidateContainer">
      <CCol
          v-for="(candidate, index) in candidates"
          :key="index"
          cols="12"
          md="4"
          class="mb-4"
      >
        <CCard class="h-100 candidate-card">
          <div class="text-center pt-3">
            <img
                :src="candidate.picture_url"
                class="img-fluid rounded"
                alt="Candidate Picture"
                style="object-fit: cover; height: 200px; width: 200px;"
            />
          </div>
          <CCardBody>
            <p><strong>No:</strong> {{ candidate.candidate_id }}</p>
            <p><strong>Name:</strong> {{ candidate.name }}</p>
            <p><strong>Score:</strong></p>
            <h4 class="text-center">{{ candidate.score }}</h4>
          </CCardBody>
        </CCard>
      </CCol>
    </CRow>
  </div>
</template>

<script>
export default {
  name: 'result_assosiation',
  data() {
    return {
      candidates: [
        {
          candidate_id: 1,
          name: 'John Doe',
          score: 120,
          picture_url:
              'https://via.placeholder.com/200x200.png?text=Candidate+1',
        },
        {
          candidate_id: 2,
          name: 'Jane Smith',
          score: 90,
          picture_url:
              'https://via.placeholder.com/200x200.png?text=Candidate+2',
        },
        {
          candidate_id: 3,
          name: 'Alice Johnson',
          score: 80,
          picture_url:
              'https://via.placeholder.com/200x200.png?text=Candidate+3',
        },
      ],
    };
  },
};
</script>

<style scoped>
.candidate-card {
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  border-radius: 15px;
  transition: box-shadow 0.3s ease;
}
.candidate-card:hover {
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.2);
}
img {
  max-width: 100%;
  height: auto;
}
</style>
