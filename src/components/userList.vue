<template>
  <div class="row">
      <renderUser class="col-12 col-md-6 col-lg-4" 
      v-on:delete-user="deleteUser"  
      v-for="(user,$index) in users" 
      v-bind:user="user" 
      v-bind:key="$index"
    />
   
    
  </div>
</template>

<script>
import renderUser from "./renderUser";

export default {
  props: ["users"],
  components: {
    renderUser
  },
  methods: {
    deleteUser(user) {
      const todoIndex = this.users.indexOf(user);
      this.users.splice(todoIndex, 1);
    },
  },
};
</script>

<style >


</style>
