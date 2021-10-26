<template>
  <l-container>
    <el-alert 
      v-if="error"
      :title="error"
      type="error">
    </el-alert>

    <el-form ref="form" :model="form" label-width="120px">
      <el-form-item label="Correo">
        <el-input v-model="email" type="email"></el-input>
      </el-form-item>
        <el-form-item label="Contraseña">
        <el-input v-model="password" type="password"></el-input>
      </el-form-item>

      <el-form-item>
        <el-button type="primary" @click="userRegister()">Registrarse</el-button>
        <el-button type="info" @click="$router.push('/login')">Volver</el-button>
      </el-form-item>
    </el-form>
  </l-container>
</template>

<script>
export default {
  auth: 'guest',
  name: 'Register',
  layout: 'form',
  middleware: 'auth',
  data() {
    return {
      email: '',
      password: '',
      error: '',
    }
  },
  methods: {
    async userRegister() {
      try {
        this.error = ''
        await this.$axios.post('http://localhost:3333/users', {
          data: this.form,
        })
        
        await this.$auth.loginWith('local', {
          data: this.form,
        })

        this.$router.push()
      } catch (err) {
        this.error = err.response.data.message
      }
    }
  },
}
</script>
