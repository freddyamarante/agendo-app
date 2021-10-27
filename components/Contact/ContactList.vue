<template>
  <div>
    <el-empty 
      v-if="contacts.length === 0"
      description="No tienes contactos añadidos"
    >
    </el-empty>
    <contact 
    v-for="contact in contacts"
    v-else-if="contacts.length !== 0" 
    :key="contact.id" 
    :contact="contact"
    @delete="$emit('delete', $event)"
    />
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
      type: Array,
      required: true,
    },
  },
  methods: {},
}
</script>
