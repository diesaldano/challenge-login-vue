<template>
  <v-layout align-center justify-center>
    <v-flex xs12 sm8 md3>
      <v-card class="cardLogin">
        <img
            class="logo"
            src="../assets/cintelink-logo-big.png"
        />
          <v-card-text>
            <v-form @submit.prevent="login" v-model="valid">
              <v-text-field
                v-model="username"
                :rules="rules.username"
                solo
                background-color="rgb(238 238 238)"
                name="login"
                label="Usuario"
                type="text"
                clearable
              />
              <v-text-field
                v-model="password"
                :rules="rules.password"
                solo
                background-color="rgb(238 238 238)"
                id="password"
                name="password"
                label="Contraseña"
                type="password"
                clearable
              />
            </v-form>
            <h3 class="errorType" v-if="error">{{errorMessage}}</h3>
          </v-card-text>
          <v-card-actions class="containerButton">
            <v-btn  class="buttonSumit" type="submit" @click="login">
              <font-awesome-icon class="pr-4" icon="fas fa-unlock-alt" />
              Login
            </v-btn>
          </v-card-actions>
          <div class="pb-10">
            <h5 style="color: #2d9cdb; font-size: 1em" class="subheading font-weight-light pt-7">¿Olvidaste tu contraseña?</h5>
            <h5 class="subheading font-weight-medium">Crear cuenta</h5>
          </div>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
export default {
  name: 'LoginBox',
  data: () => ({
    username: '',
    password: '',
    error: false,
    errorMessage: '',
    valid: false,
    rules: {
      username: [
        (v) => !!v || 'El usuario es requerido',
        (v) => (v.length >= 3 && v.length < 20) || 'El usuario debe tener ente 3 y 20 caracteres',
        (v) => /^[a-zA-Z0-9 .]+$/.test(v) || 'El usuario solo puede contener letras, números o puntos',
      ],
      password: [
        (v) => !!v || 'La contraseña es requerida',
        (v) => v.length > 8 || 'La contraseña debe tener al menos de 8 caracteres',
      ],
    }
  }),
  methods: {
    async login() {
      this.validate();
      try {
        if(this.valid){
          let res = await fetch('https://cintelink.com.ar/login.mod.php', {
            method: 'POST',
            headers: {
              'content-type': 'application/x-www-form-urlencoded',
            },
            body: JSON.stringify({
              user: this.username,
              pass: this.password,
              accion: 'LoginWSUser',
              format: 'json'
            }),
          });
          let data = await res.json();
          console.log(data);
          if(data.error) {
            this.error = true;
            this.errorMessage = data.errores.map(e => e).join(', ');
            return;
          } 
          this.$router.push('/home');
        }
      } catch (error) {
        console.log('Error encontrado: ',error);
      }
    },
    validate() {
      if(!this.username ) {
        this.error = true;
        this.errorMessage = 'No puede haber campos vacíos';
        this.valid = false;
        return;
      } else if(this.username.length < 3 || this.username.length > 20){
        this.error = true;
        this.errorMessage = 'Error en el campo usuario';
        this.valid = false;
        return;
      } else if(!this.password){
        this.error = true;
        this.errorMessage = 'No puede haber campos vacíos';
        this.valid = false;
        return;
      } else if(this.password.length < 8){
        this.error = true;
        this.errorMessage = 'Error en el campo contraseña';
        this.valid = false;
        return;
      } else {
        this.error = false;
        this.errorMessage = '';
        this.valid = true;
      }
    },
  },
};
</script>
<style>
.logo {
  margin: auto;
  padding-top: 2em;
  max-width: 150px !important;
}

.containerButton {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 0px 8px !important;
}

.buttonSumit {
  width: 120px;
  border-radius: 30px !important;
  background-color: #2d9cdb !important;
  color: white !important;
}

.errorType {
  color: rgb(230, 22, 22);
  font-size: 1.2em;
  font-weight: 400;
  padding: 0px;
}

.cardLogin {
  box-shadow: 0px 7px 8px -4px rgb(0 0 0 / 20%), 0px 12px 17px 2px rgb(0 0 0 / 14%), 0px 5px 22px 4px rgb(0 0 0 / 12%) !important;
}

  @media (max-width: 425px) {
    .cardLogin {
      box-shadow: none !important;
    }
  }

</style>
