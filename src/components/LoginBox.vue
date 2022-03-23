<template>
  <v-layout align-center justify-center>
    <v-flex xs12 sm8 md3>
      <v-card class="elevation-12">
        <img
            class="logo"
            src="../assets/cintelink-logo-big.png"
        />
          <v-card-text>
            <v-form @submit.prevent="login">
                <v-text-field
                  v-model="username"
                  solo
                  background-color="rgb(238 238 238)"
                  name="login"
                  label="Usuario"
                  type="text"
                  clearable
                />
                <v-text-field
                  v-model="password"
                  solo
                  background-color="rgb(238 238 238)"
                  id="password"
                  name="password"
                  label="Contraseña"
                  type="password"
                  clearable
                />
            </v-form>
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
  }),
  methods: {
    async login() {
      try {
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
        //this.$router.push('/home');

      } catch (error) {
        console.log('Errooor',error);
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

</style>
