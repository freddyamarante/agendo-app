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
        </el-descriptions-item>

        <el-descriptions-item  :span="3">
          <template slot="label">
            <i class="el-icon-postcard"></i>
            Para:
          </template>
        </el-descriptions-item>

        <el-descriptions-item  :span="3">
          <template slot="label">
            <i class="el-icon-postcard"></i>
            Asunto
          </template>
        </el-descriptions-item>
        
        <el-descriptions-item :span="3">
          <template slot="label">
            <i class="el-icon-document"></i>
            Texto
          </template>
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
    }
  },
  data() {
    return {
      todoData: {
        title: '',
        description: '',
        location: '',
        contactId: '',
        date: '',
        completed: false
      },
      userData: {
        email: ''
      }
    }
  },
  mounted() {
    if (this.todoId) {
      this.getTodoById()
    }
  },
  methods: {
    async getTodoById() {
      this.todoData = await this.$axios.$get(`http://localhost:3333/todos/${this.todoId}`)
    }
  }
}
</script>
