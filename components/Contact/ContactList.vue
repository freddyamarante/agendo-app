<template>
  <div>
    <contact 
      v-for="contact in contacts"
      :key="contact.id"
      :contact="contact"
    />
  </div>
</template>

<script>
export default {
  name: 'ContactList',
  props: {
    contacts: {
      type: Object,
      required: true,
    }
  }
}
</script>
