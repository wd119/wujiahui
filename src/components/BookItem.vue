<template>
  <tr 
    :class="{ active: isSelected }"
    @click="handleRowClick"
  >
    <td>{{ index + 1 }}</td>
    <td>
      <span v-if="!book.isEditing">{{ book.name }}</span>
      <input 
        v-else 
        v-model="localBook.name" 
        placeholder="请输入书名"
         @blur="saveChanges"
      >
    </td>
    <td>
      <span v-if="!book.isEditing">¥{{ book.price.toFixed(2) }}</span>
      <input 
        v-else 
        v-model.number="localBook.price" 
        type="number" 
        min="0" 
        step="0.01"
        placeholder="请输入价格"
        @blur="saveChanges"
      >
    </td>
    <td>
      <button 
        :disabled="book.count <= 1" 
        @click.stop="decreaseCount"
      >-</button>
      {{ book.count }}
      <button @click.stop="increaseCount">+</button>
    </td>
    <td>
      <button @click.stop="removeBook">移除</button>
    </td>
  </tr>
</template>

<script>
export default {
  emits: ['select', 'update','remove'],
  name: 'BookItem',
  props: {
    book: {
      type: Object,
      required: true
    },
    index: {
      type: Number,
      required: true
    },
    isSelected: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      localBook: { ...this.book }
    }
  },
  computed: {
    isValid() {
      return this.localBook.name.trim() && this.localBook.price > 0
    }
  },
  watch: { book: {
    handler(newVal) {
      this.localBook = { ...newVal };
    },
    deep: true
  }
},
  methods: {
    handleRowClick() {
      if (!this.book.isEditing) {
        this.$emit('select', this.index)
      }
    },
    increaseCount() {
      this.$emit('update', {
        index: this.index,
        book: { ...this.book, count: this.book.count + 1 }
      })
    },
    decreaseCount() {
      if (this.book.count > 1) {
        this.$emit('update', {
          index: this.index,
          book: { ...this.book, count: this.book.count - 1 }
        })
      }
    },
    
    saveChanges() {
      if (this.isValid) {
        this.$emit('update', {
          index: this.index,
          book: { ...this.localBook, isEditing: false }
        })
      }
    },
    removeBook() {
      this.$emit('remove', this.index)
    }
  }
}
</script>