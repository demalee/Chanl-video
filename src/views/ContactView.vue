<template>
<div id="contact">

  <h2>Contact Me</h2>
  <p>My name is {{name}} ,You can reach me through   phone on {{ phoneNumber }} or email {{email}}, or via my  address at Nairobi City.</p>
</div>
</template>
<script>
export default {
  name: 'ContactView',
  data() {
    return {
      phoneNumber: '0706244585',
      name:'Kibet',
      email:'dev.demalee@gmail.com'
    }
  }
}
</script>
<style scoped="">
#contact {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  padding: 2rem;
  margin: 2rem;
  max-width: 650px;
  border: 1px solid #ddd;
  border-radius: 10px;
}
h2 {
  margin: 0 0 1.5rem 0;
}
</style>
