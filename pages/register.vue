<template>
  <div class="register-form">
      <h1 class="title-form">AgenDo - Registro</h1>
      <el-alert v-for="error in errors" :key="error.message" :title="error.message" type="error"> </el-alert>

      <el-form ref="form" :model="form" label-width="120px">


            <el-form-item label="Nombre">
              <el-input v-model="form.name" type="text"></el-input>
            </el-form-item>

            <el-form-item label="Apellido">
              <el-input v-model="form.lastname" type="text"></el-input>
            </el-form-item>

            <el-form-item label="Correo">
              <el-input v-model="form.email" type="email"></el-input>
            </el-form-item>

            <el-form-item label="Pais">
              <el-input v-model="form.country" type="text"></el-input>
            </el-form-item>
            <el-form-item label="Ciudad">
              <el-input v-model="form.city" type="text"></el-input>
            </el-form-item>
            <el-form-item label="Contraseña">
              <el-input v-model="form.password" type="password"></el-input>
            </el-form-item>


          <el-form-item>
            <el-button type="warning" @click="userRegister()"
              >Registrarse</el-button>
            <el-button type="info" @click="$router.push('/login')"
              >Volver</el-button>
          </el-form-item>
      </el-form>
  </div>
</template>

<script>
export default {
  auth: 'guest',
  name: 'Register',
  layout: 'form',
  middleware: 'auth',
  data() {
    return {
      form: {
        name: '',
        lastname: '',
        email: '',
        country: '',
        city: '',
        password: '',
      },
      errors: [],
    }
  },
  methods: {
    async userRegister() {
      try {
        const data = this.form
        await this.$axios.post('http://localhost:3333/users', data)

        await this.$auth.loginWith('local', {
          data: this.form,
        })

        await this.$router.push('/')
      } catch (err) {
        
        this.errors = await err.response.data.errors
        console.log(err.response.data.errors)
      }
    },
  },
}
</script>

<style>
.register-form {
  left: 50%;
  top: 50%;
}

.title-form {
  text-align: center;
}
</style>