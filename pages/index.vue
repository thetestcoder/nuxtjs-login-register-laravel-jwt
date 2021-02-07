<template>
  <div class="container">
    <h2>Login System</h2>
    <div>
      <nuxt-link to="/login">Login</nuxt-link>
      <nuxt-link to="/register">Register</nuxt-link>
    </div>
  </div>
</template>

<script>
export default {
  head: {
    title: process.env.PROJECT_NAME ,
  },
}
</script>
