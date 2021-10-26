<template>
  <el-card
    v-loading="loading"
    class="row-bg box-card"
    shadow="hover"
    :body-style="{ padding: '0px' }"
  >
    <el-form ref="form" :model="form">
      <el-descriptions border>
        <el-descriptions-item :span="3">
          <template slot="label">
            <i class="el-icon-postcard"></i>
            Título
          </template>
          <el-input v-model="form.title" clearable> </el-input>
        </el-descriptions-item>
        <el-descriptions-item :span="3">
          <template slot="label">
            <i class="el-icon-document"></i>
            Descripción
          </template>
          <el-input v-model="form.description" clearable> </el-input>
        </el-descriptions-item>
        <el-descriptions-item :span="3">
          <template slot="label">
            <i class="el-icon-location-outline"></i>
            Lugar
          </template>
          <el-input v-model="form.location" clearable> </el-input>
        </el-descriptions-item>
        <el-descriptions-item :span="3">
          <template slot="label">
            <i class="el-icon-user"></i>
            Contacto
          </template>
          <el-select v-model="form.contactId" placeholder="Select"  clearable @change="$forceUpdate()">
            <el-option
              v-for="contact in contactOptions"
              :key="`contact_select_${contact.id}`"
              :label="`${contact.name} ${contact.lastname}`"
              :value="contact.id"
            >
            </el-option>
          </el-select>
        </el-descriptions-item>
        <el-descriptions-item :span="3">
          <template slot="label">
            <i class="el-icon-date"></i>
            Fecha
          </template>
          <div class="block">
            <el-date-picker
              v-model="form.date"
              type="date"
              placeholder="Escoge fecha"
              format="dd.MM.yyyy"
            >
            </el-date-picker>
          </div>
        </el-descriptions-item>
      </el-descriptions>
      <el-form-item>
        <el-button v-if="type === 'create'" type="primary" @click="addTodo()"
          >Añadir Agenda</el-button>
        <el-button v-if="type === 'update'" type="primary" @click="updateTodo()"
          >Editar Agenda</el-button
        >
      </el-form-item>
    </el-form>
  </el-card>
</template>

<script>
import moment from 'moment'

export default {
  name:'TodoForm',
  props: {
    todoId: {
      type: String,
      default: null,
      },
    type: {
      type: String,
      default: 'create'
    }
  },
  data() {
    return {
      form: {
        title: '',
        description: '',
        location: '',
        contactId: '',
        date: '',
        completed: false
      },
      contactOptions: [],
      loading: false
    }
  },
  mounted() {
    if (this.todoId) {
    this.getTodoById()
    }
    this.getContacts()
  },
  methods: {
    async getContacts() {
      this.contactOptions = await this.$axios.$get('http://localhost:3333/contacts')
    },

    async addTodo() {
      this.loading = true
      const data = this.normalize(this.form)
      await this.$axios.$post('http://localhost:3333/todos', data)
      this.loading = false
      this.$router.push('/')
      this.$notify({
        title: 'Agenda añadida',
        type: 'success'
      })
    },

    async updateTodo() {
      const data = this.normalize(this.form)
      await this.$axios.$put('http://localhost:3333/todos', data)
      this.$router.push('/')
      this.$notify({
        title: 'Agenda editada',
        type: 'success'
      })
    },

    normalize(data) {
      const date = new Date(data.date)
      data.date = date.toLocaleDateString('fr-CH')
      return data
    },

    async getTodoById() {
      this.form = await this.$axios.$get(`http://localhost:3333/todos/${this.todoId}`)
      this.form.contactId = this.form.contact_id
      delete this.form.contact_id
      this.form.date = moment(this.form.date, 'dd.MM.yyyy')
    }
  }
}
</script>