<template>
  <div>
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
  </div>
</template>

<script>
export default {
  name: 'Login',
  layout: 'form',
  data() {
    return {
      form: {
        email: '',
        password: '',
        rememberMe: false,
      },
    }
  },
  methods: {
    async userLogin() {
      this.message = null;
      this.errors = [];
      
      try {
        const response = await this.$auth.loginWith('local', {
          data: this.form,
        })
        console.log(response)
      } catch (err) {
        console.log(err)
      }
    },
  },
}
</script>