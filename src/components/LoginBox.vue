<template>
  <v-layout align-center justify-center>
    <v-flex xs12 sm8 md3>
      <v-card class="elevation-12">
        <img
            class="logo"
            src="../assets/cintelink-logo-big.png"
        />
          <v-card-text>
            <v-form>
                <v-text-field
                  solo
                  background-color="rgb(238 238 238)"
                  name="login"
                  label="Usuario"
                  type="text"
                  clearable
                ></v-text-field>
                <v-text-field
                  solo
                  background-color="rgb(238 238 238)"
                  id="password"
                  name="password"
                  label="Contraseña"
                  type="password"
                  clearable
                ></v-text-field>
            </v-form>
          </v-card-text>
          <v-card-actions class="containerButton">
            <v-btn color="primary" to="/">Login</v-btn>
          </v-card-actions>
          <div>
            <h5>¿Olvidaste tu contraseña?</h5>
            <h5>Crear cuenta</h5>
          </div>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
export default {
  name: 'LoginBox',
  data: () => ({
    //
  }),
};
</script>
<style>
.logo {
  margin: auto;
  padding-top: 2em;
  max-width: 180px !important;
}

.containerButton {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 0px 8px !important;
}

</style>
