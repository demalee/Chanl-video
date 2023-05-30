<template>
  <div>

    <ChanlVideo @clip-submitted="handleClipSubmitted" />
    <!-- Card displaying clip parameters -->
    <div class="card">
      <div class="card-body">
        <h5 class="card-title">Chanl Clip Parameters</h5>
        <p class="card-text">
          <strong>Download:</strong> {{ clipParams.download }}
        </p>
        <p class="card-text">
          <strong>Start Time:</strong> {{ clipParams.start }}
        </p>
        <p class="card-text">
          <strong>End Time:</strong> {{ clipParams.end }}
        </p>
        <p class="card-text">
          <strong>Title:</strong> {{ clipParams.title }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
// The handleClipSubmitted method   stores the clip parameters in a data property.
import ChanlVideo from '@/components/ChanlVideo.vue';

export default {
  name: "HomePage",
  components: {
    ChanlVideo
  },
  data() {
    return {
      clipParams: {
        download: "",
        start: "",
        end: "",
        title: "",

      },

    };
  },
  methods: {
    handleClipSubmitted(clipParams) {
      // Update the clipParams data property
      this.clipParams = clipParams;
    },
  },


};
</script>
<style scoped>
#card {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;

  margin: 2rem;
  border-radius: 14px;
  max-width: 400px;
  border: 1px solid #ddd;
  display: flex;
  border-bottom: 5px solid #ddd;
  justify-content: space-between;
  border-bottom: 1px solid #ddd;
}
</style>