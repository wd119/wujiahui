<template>
    <div class="header">
        <h2>{{ title }}</h2>
        <slot name="left"></slot>
    </div>
</template>
<script>
export default {
    name: 'HeaderSection',
    props: {
        title: {
            type: String,
            required: true
        }
}
}
</script>
<style scoped>
.section-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 30px 0 20px;
  padding-bottom: 10px;
  border-bottom: 1px solid #eee;
}

.section-header h2 {
  font-size: 20px;
  font-weight: 600;
  color: #333;
}
</style>