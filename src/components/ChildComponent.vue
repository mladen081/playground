<template setup>
  <p>{{ msg || 'No props passed yet' }}</p>
</template>

<script setup>
const { msg } = defineProps({
  msg: String
})

const emit = defineEmits(['response'])

emit('response', 'hello from child')
</script>
