<template>
<div class="container">
  <div class="row">
    <div class="col-md-6 offset-md-3">
      <table class="table table-hover table-bordered">
        <tr>
          <th>Name</th>
          <td>{{user.name}}</td>
        </tr>
        <tr>
          <th>Email</th>
          <td>{{user.email}}</td>
        </tr>
        <tr>
          <th>Created Date</th>
          <td>{{user.created_at}}</td>
        </tr>
      </table>
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: "Profile",
  middleware:'auth',
  head: {
    title: "Profile - " + process.env.PROJECT_NAME ,
  },
  computed:{
    user(){
      return this.$auth.user;
    }
  }
}
</script>

<style scoped>

</style>
