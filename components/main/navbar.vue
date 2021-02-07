<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container-fluid">
      <nuxt-link class="navbar-brand" to="/">NuxtJS Auth</nuxt-link>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <nuxt-link class="nav-link active" aria-current="page" to="/">Home</nuxt-link>
          </li>
        </ul>
        <div class="mr-0">
          <div v-if="!$auth.loggedIn">
            <nuxt-link to="/login" class="btn btn-primary">Login</nuxt-link>
            <nuxt-link to="/register" class="btn btn-primary">Register</nuxt-link>
          </div>
         <div v-else>
           <nuxt-link to="/profile">{{$auth.user ? $auth.user.name : ""}}</nuxt-link>
           <button class="btn btn-primary" @click="logout">Logout</button>
         </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: "navbar",
  methods:{
    async logout(){
      try{
        await this.$auth.logout();
        this.$toast.success("Successfully logged out!")
      }catch (e) {
        this.$toast.error("Unable to logout!");
      }
    }
  }
}
</script>
