<template>
  <div class="card-footer text-muted">
    <span class="footer"
      >COPYRIGHT © {{ fullYear }} DESIGNED BY DEEPTA BARUA</span
    >
  </div>
</template>

<script>
export default {
  name: "Footer",
  data() {
    return {
      fullYear: new Date().getFullYear(),
    };
  },
};
</script>

<style scoped>
.card-footer {
  background-color: white;
}
.footer {
  color: black !important;
  font-size: 12px !important;
}
</style>