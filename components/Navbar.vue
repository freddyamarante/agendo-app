<template>
  <el-menu :default-active="$route.path" class="el-menu-demo" mode="horizontal" @select="handleSelect">
    <el-menu-item :disabled="!$auth.loggedIn" index="/" @click="$router.push('/')">Inicio</el-menu-item>
    <el-menu-item :disabled="!$auth.loggedIn" index="/todo/create" @click="$router.push('/todo/create')">Crear Agenda</el-menu-item>
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
      handleClick(tab, event) {
        console.log(tab, event)
      },
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
