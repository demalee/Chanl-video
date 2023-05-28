<template>
<div id="contact">
  <img alt="Our Logo" src="../assets/logo.png">

  <h2>Contact us</h2>
  <p>My name is {{name}} Contact me  by phone on {{ phoneNumber }}, or via my  address at Nairobi City.</p>
</div>
</template>
<script>
export default {
  name: 'ContactView',
  data() {
    return {
      phoneNumber: '0706244585',
      name:'Kibet'
    }
  }
}
</script>
<style scoped="">
#contact {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  padding: 2rem;
  margin: 2rem;
  border: 1px solid #ddd;
  border-radius: 10px;
}
h2 {
  margin: 0 0 1.5rem 0;
}
</style>
