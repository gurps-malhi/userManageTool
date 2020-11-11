<template>
    <div class="content">
        <!-- // user shown when we are not in editing mode. -->
        <div class="card-deck">
        <div class="card mb-4" v-show="!isEditing">
            <div class="card-body">
            <h2 class="header2 mb-0">{{ user.firstName }} {{ user.lastName }}</h2>
            <p class="font-weight-light">
                {{ user.jobRole }}
            </p>
            <div class="">
                {{ user.address }}
            </div>
            </div>
            <div class="card-footer">
            <button
                v-on:click="showForm(user)"
                class="text-white btn-rounded primary-bg px-3 mr-3"
            >
                Edit<i class="ml-2 fas fa-edit"></i>
            </button>
            <button
                v-on:click="deleteUser(user)"
                class="btn-rounded primary-color px-3"
            >
                Delete<i class="ml-2 far fa-trash-alt"></i>
            </button>
            </div>
        </div>
        </div>

        <!-- // form is visible when we are in editing mode -->
        <div class="card-deck">
        <div class="card mb-4" v-show="isEditing">
            <div class="card-body p-3">
            <div class="form">
                <div class="primary-bg py-2 rounded mb-2"><h3 class="text-white text-center">Edit user <i class="far fa-user" aria-hidden="true"></i></h3></div>
                <div class="form-group">
                <label>First Name</label>
                <input
                    type="text"
                    class="form-control"
                    v-model="confirmEdit.firstName"
                />
                </div>
                <div class="form-group">
                <label>Last Name</label>
                <input
                    type="text"
                    class="form-control"
                    v-model="confirmEdit.lastName"
                />
                </div>
                <div class="form-group">
                <label>Job Role</label>
                <input
                    type="text"
                    class="form-control"
                    v-model="confirmEdit.jobRole"
                />
                </div>
                <div class="form-group">
                <label>Address</label>
                <input
                    type="text"
                    class="form-control"
                    v-model="confirmEdit.address"
                />
                </div>
            </div>
            </div>
            <div class="card-footer">
            <button
                class="text-white btn-rounded primary-bg px-3 mr-3"
                v-on:click="hideForm()"
            >
                Cancel
            </button>
            <button
                class="btn-rounded primary-color px-3"
                v-on:click="confirmForm(user)"
            >
                Save
            </button>
            </div>
        </div>
        </div>
    </div>
</template>

<script>
export default {
  props: ["user"],
  data() {
    return {
      isEditing: false,
      confirmEdit: {
        firstName: "",
        lastName: "",
        jobrole: "",
        address: "",
        done: false
      }
    };
  },
  methods: {
    showForm(user) {
      this.isEditing = true;
      this.confirmEdit.firstName = user.firstName;
      this.confirmEdit.lastName = user.lastName;
      this.confirmEdit.jobRole = user.jobRole;
      this.confirmEdit.address = user.address;
    },
    hideForm() {
      this.isEditing = false;
    },
    confirmForm(user) {
      user.firstName = this.confirmEdit.firstName;
      user.lastName = this.confirmEdit.lastName;
      user.jobRole = this.confirmEdit.jobRole;
      user.address = this.confirmEdit.address;
      this.isEditing = false;
    },
    deleteUser(user) {
      this.$emit("delete-user", user);
    }
  }
};
</script>

<style lang="scss">
.button[disabled] {
  cursor: not-allowed;
}
i {
  cursor: pointer;
}
.content {
  color: $primary;
}
</style>
