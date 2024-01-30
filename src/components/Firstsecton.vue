<template>
  <div class="cont">
    <v-card class="pa-10 d-flex flex-column justify-left">
      <span
        class="card-title text-light-blue-darken-4 font-weight-bold mb-2 pa-0"
        >Not a Navy Federal Member?</span
      >
      <p
        class="line-spacing text-light-blue-darken-4 text-h5 font-weight-medium mb-4 pa-0"
      >
        Join now and enjoy the support and great service of a credit union that
        puts your needs first.
      </p>
      <v-card-actions class="actions my-5 ga-2 pa-0">
        <button
          class="btn-1 px-6 py-4 ma-1 bg text-subtitle-1 rounded-lg font-weight-bold text-white"
        >
          Become a Member
        </button>
        <button
          class="btn-2 px-6 py-4 ma-1 text-subtitle-1 rounded-lg font-weight-bold text-white"
        >
          Learn More
        </button>
      </v-card-actions>
    </v-card>
  </div>
</template>
  
  <script setup>
</script>
  
<style scoped>
.card-title {
  font-size: 5.6vw;
}
.line-spacing {
  line-height: 1.5;
}
.actions {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  width: 100%;
}

.actions button {
  padding: 10px;
}

.btn-1 {
  background-color: #b54e00;
}
.btn-2 {
  background-color: #0057ba;
}

@media screen and (min-width: 500px) {
  .card-title {
    font-size: 4vw;
  }
}
</style>