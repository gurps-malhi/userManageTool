<template>
  <div class="row">
    <div class="col-12 mx-auto">
        <button class="text-white btn-rounded primary-bg px-5 py-2 mx-auto d-block header2 col-12 col-md-4 col-lg-3 font-weight-bold" v-on:click="openForm" v-show="!isCreating">Create a new user
        <i class="fas fa-user-plus"></i>
        </button>
        <div class="card-deck central-pos col-12 col-md-6 col-lg-6 col-xl-4">
            <div class="card box-shadow" v-show="isCreating">
                <div class="card-body">
                    <div class="form">
                        <div class="primary-bg py-2 rounded mb-2">
                            <h3 class="text-white text-center">Create new user <i class="far fa-user"></i></h3>
                        </div>
                        <div class="form-group">
                            <label>First Name (*):</label>
                            <input class="form-control" v-model="userFirstName" type="text" ref="firstName" defaultValue="">
                        </div>
                        <div class="form-group">
                            <label>Last Name (*):</label>
                            <input class="form-control" v-model="userLastName" type="text" ref="lastName" defaultValue="">
                        </div>
                        <hr>
                        <div class="form-group">
                            <label>Job Role (*):</label>
                            <input class="form-control" v-model="userJobRole" type="text" ref="jobRole" defaultValue="">
                        </div>
                        <div class="form-group">
                            <label>Address (*):</label>
                            <input class="form-control" v-model="userAddress" type="text" ref="userAddress" defaultValue="">
                        </div>
                    </div>
                </div>
                <div class="card-footer">
                    <div class="" v-show="showErrorMsg">
                      <p class="text-alert alert-text">Please populate empty field(s)</p>
                    </div>
                        <button class="text-white btn-rounded primary-bg px-3 mr-3" v-on:click="sendForm">
                        Create
                        </button>
                        <button class="btn-rounded primary-color px-3" v-on:click="closeForm">
                        Cancel
                        </button>
                </div>

            </div>
        </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      userFirstName: "",
      userLastName: "",
      userJobRole: "",
      userAddress: "",
      isCreating: false,
      showErrorMsg: false,
    };
  },
  methods: {
    openForm() {
      this.isCreating = true;
    },
    closeForm() {
      this.isCreating = false;
      this.showErrorMsg = false;
    },
    sendForm() {
      if (this.userFirstName.length > 0 && 
          this.userLastName.length > 0 &&
          this.userJobRole.length > 0 &&
          this.userAddress.length > 0) {
          const firstName = this.userFirstName;
          const lastName = this.userLastName;
          const jobRole = this.userJobRole;
          const address = this.userAddress;
          this.$emit("create-todo", {
          firstName,
          lastName,
          jobRole,
          address,
          done: false
        });
        this.userFirstName = "";
        this.userLastName = "";
        this.userJobRole = "";
        this.userAddress = "";
        this.isCreating = false;
        this.showErrorMsg = false;
      }else{
        this.showErrorMsg = true;
      }
    }
  }
};
</script>

