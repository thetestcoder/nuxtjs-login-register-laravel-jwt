<template>
<div class="container mt-3">
  <div class="row">
    <h2 class="text-white bg-success p-2 rounded text-center">Login</h2>
    <div class="col-md-6 offset-md-3">
      <div class="mb-2">
        <label for="email" class="form-label">Email</label>
        <input type="email" id="email" class="form-control" v-model="userLogin.email">
      </div>
      <div class="mb-2">
        <label for="password" class="form-label">Password</label>
        <input type="password" id="password" class="form-control" v-model="userLogin.password">
      </div>
      <div class="d-grid mb-2">
        <button class="btn btn-success" @click="login">Login</button>
      </div>
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: "Login",
  middleware:'guest',
  head: {
    title: "Login -" + process.env.PROJECT_NAME ,
  },
  data(){
    return{
      userLogin:{
        email:"",
        password:""
      }
    }
  },
  methods:{
    async login(){
      try{
        this.$toast.show("Logging In.....")
        let res = await this.$auth.loginWith('laravelJWT', {
          data:{
            email:this.userLogin.email,
            password:this.userLogin.password
          }
        });
        this.$toast.success("Successfully logged In")
      }catch (e){
        if (e.response.status === 401){
          this.$toast.error("Check Your Email and Password")
        }else{
          this.$toast.error("Unable to login")
        }
      }
    }
  }
}
</script>
