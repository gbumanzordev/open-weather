<template>
  <p>Get location comp</p>
  <p v-if="gettingLocation">Loading location...</p>
</template>

<script>
export default {
  name: "LocalWeather",
  data() {
    return { location: null, gettingLocation: false, error: null };
  },
  async mounted() {
    await this.getLocation();
  },
  methods: {
    async getLocation() {
      if (!("geolocation" in navigator)) {
        this.error = "Geolocation is not available";
        return;
      }
      this.gettingLocation = true;

      navigator.geolocation.getCurrentPosition(
        (position) => {
          this.gettingLocation = false;
          this.location = position;
        },
        (error) => {
          this.gettingLocation = false;
          this.error = error.message;
        }
      );
    },
  },
};
</script>

<style scoped></style>
