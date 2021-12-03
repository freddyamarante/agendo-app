<template>
  <el-menu 
    :default-active="$route.path" 
    mode="horizontal"
    background-color="#fce181"
    text-color="#00000"
    active-text-color="#00000"
    >
    <el-menu-item :disabled="!$auth.loggedIn" index="/" @click="$router.push('/')">Inicio</el-menu-item>
    <el-menu-item :disabled="!$auth.loggedIn" index="/todo/completed" @click="$router.push('/todo/completed')">Completados</el-menu-item>
    <el-menu-item v-if="$auth.loggedIn" @click="confirmLogout()">
      Logout
    </el-menu-item>
  </el-menu>
</template>

<script>
  export default {
    data() {
      return {
        activeName: 'first',
      }
    },
    methods: {
      logout() {
        this.$auth.logout()
          .then(() => {
            this.$router.push('/login')
          })
      },
      confirmLogout() {
        this.$confirm('¿Estás seguro que deseas cerrar sesión?', 'Warning', {
          confirmButtonText: 'Si',
          cancelButtonText: 'No',
          type: 'warning'
        }).then(() => {
          this.logout()
          this.$message({
            type: 'success',
            message: 'Cierre de sesión exitoso'
          });
        })      
      }
    },
  }
</script>

<style scoped>
.el-menu {
  width:100%;
  color:black
}
</style>
