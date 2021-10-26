<template>
  <l-container>
    <el-alert 
      v-if="error"
      :title="error"
      type="error">
    </el-alert>

    <el-form ref="form" :model="form" label-width="120px">
      <el-form-item label="Correo">
        <el-input v-model="form.email" type="email"></el-input>
      </el-form-item>
      <el-form-item label="Contraseña">
        <el-input v-model="form.password" type="password"></el-input>
      </el-form-item>
    
      <el-form-item>
        <el-button type="primary" @click="userLogin()">Iniciar Sesión</el-button>
        <el-button type="info" @click="$router.push('/register')">Registrarse</el-button>
      </el-form-item>  
    </el-form>
  </l-container>
</template>

<script>
export default {
  auth: 'guest',
  name: 'Login',
  layout: 'form',
  middleware: 'auth',
  data() {
    return {
      form: {
        email: '',
        password: '',
        rememberMe: false,
      },
      error: ''
    }
  },
  methods: {
    async userLogin() {
      try {
        this.error = ''
        await this.$auth.loginWith('local', {
          data: this.form,
        })
        this.$router.push('/')
        this.$notify({
          title: 'Inicio de sesión exitoso',
          message: 'Haz iniciado sesión',
          type: 'success'
        });
      } catch (err) {
        this.error = err.response.data
      }
    }
  }
}
</script>