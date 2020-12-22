<template>

  <div class="container mt-5 col-3" >
    <form>
      <div class="form-group">
        <label for="exampleInputEmail1">Correo electronico</label>
        <input
          v-model="login.email"
          type="email"
          class="form-control"
          id="exampleInputEmail1"
          aria-describedby="emailHelp"
        />
        
      </div>
      <div class="form-group">
        <label for="exampleInputPassword1">Contraseña</label>
        <input
          v-model="login.password"
          type="password"
          class="form-control"
          id="exampleInputPassword1"
        />
      </div>
      <button @click.prevent="loginUser" type="submit" class="btn btn-primary">
        Ingresar
      </button>
    </form>
  </div>
<!-- </div> -->
  
</template>


<script>
const qs = require('querystring')
import swal from 'sweetalert'
export default {
  name: "TheLogin",
  data() {
    return {
      login: {
        email: '',
        password: '',
      }
    }
  },
  methods: {
    async loginUser() {
      try {

// const config = {
//           headers: {
//             "Content-Type": "application/x-www-form-urlencoded",
//           },
//         };
        
        // let response = await this.$http.post("/api/user/login", qs.stringify(this.login), config);

        let response = await this.$http.post("/api/user/login", this.login);

        //console.log(response.data)
        let token = response.data.tokenReturn;
        let user = response.data.user;

        localStorage.setItem("jwt", token);
        localStorage.setItem("user", JSON.stringify(user));

        if (token) {
            swal("Exito!!","Login correcto","success");
          this.$router.push("/home");
        }
      } catch (e) {
        //console.log(err.response)
        swal("Oops","Algo salio mal","error")
      }
    },
  },
};
</script>

<style scoped>
.container{
  background-color: #34373B;
}
.form-group{
  color: #6DF3A3;
}
.btn-primary{
  background: #5EB3E3;
}




</style>