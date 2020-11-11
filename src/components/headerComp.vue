<template>
  <div class="row">
      <div class="col-12 mx-auto primary-bg rounded mb-5 d-inline-block">
       <h1 class="text-center text-md-left text-white my-3 col-12 col-md-9 d-inline-block"><i class="far fa-user mr-3"></i>User Management</h1>   
      <h3 class="text-white col-12 col-md-3 d-inline-block text-center text-md-right">{{users.length}} Users</h3>
      </div>
  </div>
</template>

<script>
export default {
    props:["users"]

}
</script>

<style>

</style>