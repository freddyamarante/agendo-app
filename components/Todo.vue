<template>
  <el-row>
    <el-col>
      <el-card shadow="hover">
        <el-row>
          <el-col :span="4">
            {{todo.title}}
          </el-col>
          <el-col :span="4">
            {{todo.description}}
          </el-col>
          <el-col :span="4">
            {{todo.contact.name}}
          </el-col>
          <el-col :span="4">
            {{todo.location}}
          </el-col>
          <el-col :span="4">
            {{todo.date}}
          </el-col>
          <el-col :span="4">
            {{todo.completed}}
          </el-col>
        </el-row>
      </el-card>
    </el-col>
  </el-row>
</template>

<script>
  export default {
    name: 'Todo',
    props: {
      todo: {
        type: Object,
        required: true
      }
    },  
  }
</script>
