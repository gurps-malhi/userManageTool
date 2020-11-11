<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-12 col-sm-11 mx-auto my-3">
        <headerComp :users="users"/>
        <userList :users="users"/>
        <createUser v-on:create-todo="addTodo($event)"  />
        <footerComp/>
      </div>
    </div>
  </div>
</template>

<script>
import headerComp from "./components/headerComp.vue";
import userList from "./components/userList.vue";
import createUser from "./components/createUser.vue";
import footerComp from "./components/footerComp.vue";
import usersDefault from "./usersDefault";

export default {
  name: "app",
  components: {
    userList,
    createUser,
    footerComp,
    headerComp
  },
  data() {
    return {
      users:  usersDefault.users,
    };
  },
  methods: {
    addTodo(todo) {
      this.users.push(todo);
         
    },
    saveUsers() {
      let parsed = JSON.stringify(this.users);
      localStorage.setItem('storedUsers', parsed);
    },
  },
  mounted(){  
       if(localStorage.getItem('storedUsers')) {
      try {
        this.users= JSON.parse(localStorage.getItem('storedUsers'));
      } catch(e) {
        localStorage.removeItem('storedUsers');
      }
    }
  },
  watch:{
    users:{
        handler(){
        this.saveUsers();
      }, deep:true
    }
    
 
  },
  computed:{

    
  },
};
</script>

<style >
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
