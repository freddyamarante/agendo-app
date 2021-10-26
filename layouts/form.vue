<template>
  <div>
    <el-container>
      <el-header>
        <Navbar />
      </el-header>
      <el-main>
        <el-row :gutter="20">
          <el-col :span="12" :offset="6">
            <Nuxt />
          </el-col>
        </el-row>
      </el-main>
    </el-container>
  </div>
</template>