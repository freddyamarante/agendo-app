<template>
  <div>
    <contact v-for="contact in contacts" :key="contact.id" :contact="contact" />
    <el-button
      type="primary"
      icon="el-icon-plus"
      circle
      @click="$router.push('/contact/create')"
    ></el-button>
  </div>
</template>

<script>
export default {
  name: 'ContactList',
  props: {
    contacts: {
      type: Object,
      required: true,
    },
  },
  methods: {},
}
</script>
