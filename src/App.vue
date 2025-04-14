<template>
  <div id="app">
    <BookList />
  </div>
</template>

<script>
import BookList from './components/BookList.vue'

export default {
  name: 'App',
  components: {
    BookList
  }
}
</script>

<style>
table {
  border-collapse: collapse;
  width: 100%;
}
thead {
  background-color: #ccc;
}
th, td {
  border: 1px solid #ddd;
  padding: 8px 16px;
}
.active {
  background-color: #90b54b;
  color: #fff;
}
button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
.summary {
  margin: 20px 0;
}
.add-controls {
  margin-top: 10px;
}
</style>