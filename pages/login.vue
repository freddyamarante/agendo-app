<template>
  <v-container>
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
      <el-form-item label="Recordarme">
        <el-checkbox v-model="form.rememberMe"></el-checkbox>
      </el-form-item>
        <el-button type="primary" @click="userLogin()">Iniciar Sesion</el-button>
      <el-button>Cancel</el-button>
    </el-form>
  </v-container>
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
        const response = await this.$auth.loginWith('local', {
          data: this.form,
        })
        this.$router.push('/')
        this.$notify({
          title: 'Success',
          message: 'This is a success message',
          type: 'success'
        });
        console.log(response)
      } catch (err) {
        this.error = err.response.data
      }
    }
  }
}
</script>