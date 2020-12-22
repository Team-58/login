<template>
  <div class="total">
    <nav class="navbar navbar-expand-lg navbar-light">  
      <div class="row collapse navbar-collapse" id="navbarSupportedContent">
        <form class="form-inline my-2 my-lg-0 offset-md-11">
          <button
            class="btn btn-outline-success my-2 my-sm-0 "
            type="submit"
            @click.prevent="logOut"
          >
            Salir
          </button>
        </form>
      </div>
    </nav>

    <div class="container mt-5">
      <div class="card container" style="width: 18rem">
        <ul class="list-group list-group-flush">
          <li class="list-group-item">Usuario: {{ user.username }}</li>
          <li class="list-group-item">Correo: {{ user.email }}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      user: {},
    };
  },
  methods: {
    getUserDetails() {
      let token = localStorage.getItem("jwt");
      let user = localStorage.getItem("user");

      if (token) {
        this.user = JSON.parse(user);
      }
    },
    logOut() {
      localStorage.removeItem("jwt");
      localStorage.removeItem("user");
      this.$router.push("/");
    },
  },
  created() {
    this.getUserDetails();
  },
};
</script>

<style scoped>
.container {
  color: #6df3a3;
}
.total {
  background: #34373b;
}

#navbarSupportedContent{
  background: #6df3a3;
}

.navbar{
  background:  #6df3a3;
}

.btn{
  background:   #34373b;
  color: #6df3a3;
}
</style>