<template>
  <div class="container mt-3">
    <div class="row">
      <h2 class="text-white bg-success p-2 rounded text-center">Register</h2>
      <div class="col-md-6 offset-md-3">
        <div class="mb-2">
          <label for="name" class="form-label">Name</label>
          <input type="text" id="name" class="form-control" v-model="userRegister.name">
        </div>
        <div class="mb-2">
          <label for="email" class="form-label">Email</label>
          <input type="email" id="email" class="form-control" v-model="userRegister.email">
        </div>
        <div class="mb-2">
          <label for="password" class="form-label">Password</label>
          <input type="password" id="password" class="form-control" v-model="userRegister.password">
        </div>
        <div class="d-grid mb-2">
          <button class="btn btn-success" @click="register">Register</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Register",
  middleware:'guest',
  head: {
    title: "Register - " + process.env.PROJECT_NAME ,
  },
  data(){
    return{
      userRegister:{
        name:"",
        email:"",
        password:""
      }
    }
  },
  methods:{
    async register(){
      try{
        this.$toast.show("Signing Up.....")
        await this.$axios.post("/register", this.userRegister);
        await this.$auth.loginWith('laravelJWT', {
          data:{
            email:this.userRegister.email,
            password:this.userRegister.password
          }
        });
        this.$toast.success("Successfully Registered")
      }catch (e){
        if (e.response.status === 401){
          this.$toast.error("Check Your Email and Password")
        }else{
          this.$toast.error("Unable to Register")
        }
      }
    }
  }
}
</script>
