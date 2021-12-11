<template>
    <div>
    <el-card
      class="row-bg box-card"
      shadow="hover"
      :body-style="{ padding: '0px' }"
    >
      <el-descriptions :column="3" border>
        <el-descriptions-item  :span="3">
          <template slot="label">
            <i class="el-icon-postcard"></i>
            De:
          </template>
          {{ emailData.user.email }}
        </el-descriptions-item>

        <el-descriptions-item  :span="3">
          <template slot="label">
            <i class="el-icon-postcard"></i>
            Para:
          </template>
          {{ emailData.contact.email }}
        </el-descriptions-item>

        <el-descriptions-item  :span="3">
          <template slot="label">
            <i class="el-icon-postcard"></i>
            Asunto
          </template>

          {{ `Recordatorio: ${emailData.title}`}}
        </el-descriptions-item>
        
        <el-descriptions-item :span="3">
          <template slot="label">
            <i class="el-icon-document"></i>
            Texto
          </template>
          <el-input
            v-model="textarea"
            type="textarea"
            :rows="16"
          >
          </el-input>
        </el-descriptions-item>
      </el-descriptions>
    </el-card>
  </div>
</template>

<script>
export default {
  name: 'TodoEmail',
  props: {
    todoId: {
      type: String,
      default: null,
    },
  },
  data() {
    return {
      emailData: {
        user: {
          email: ''
        },
        title: '',
        description: '',
        location: '',
        contactId: '',
        contact: {
          name: '',
          lastname: '',
          email: '',
          phone: ''
        },
        date: '',
        completed: false
      },
      textarea: ``
    }
  },
  mounted() {
    if (this.todoId) {
      this.getTodoById() 
    }
    
  },
  methods: {
    async getTodoById() {
      this.emailData = await this.$axios.$get(`http://localhost:3333/todos/${this.todoId}`)
      this.textarea = this.defaultMessage()
    },

    defaultMessage() {
      const message = `Hola, ${this.emailData.contact.name}\n\nEnvío este mensaje con la finalidad de hacerte recordar de la actividad: ${this.emailData.title}\n\nDescripción: ${this.emailData.description}\n\nFecha: ${this.emailData.date}\n\nLugar: ${this.emailData.location}\n\nEspero tu pronta respuesta,\n\nSaludos,\n\n${this.emailData.user.name} ${this.emailData.user.lastname}`
      return message
    }
  }
}
</script>
