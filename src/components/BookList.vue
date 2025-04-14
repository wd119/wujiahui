<template>
  <div class="book-cart">
    <template v-if="books.length > 0">
      <table>
        <thead>
          <tr>
            <th>序号</th>
            <th>书名</th>
            <th>价格</th>
            <th>购买数量</th>
            <th>操作</th>
          </tr>
        </thead>
        <tbody>
          <BookItem 
            v-for="(book, index) in books" 
            :key="book.id"
            :book="book"
            :index="index"
            :is-selected="currentIndex === index"

            @select="handleSelect"
            @update="handleUpdate"
            @remove="handleRemove"
          />
        </tbody>
      </table>
      
      <div class="summary">
        <p>总计：{{ formatPrice(totalPrice) }}</p>
        <p v-if="currentIndex !== -1">当前选中的书籍：{{ selectedBookName }}</p>
      </div>
      
      <button @click="addBook" v-if="showAddButton">添加书籍</button>
      <div v-else class="add-controls">
        <button @click="confirmAdd" >确认</button>
        <button @click="cancelAdd">取消</button>
      </div>
    </template>
    
    <template v-else>
      <p>购物车为空，请添加书籍</p>
      <button @click="addBook">添加书籍</button>
    </template>
  </div>
</template>

<script>
import BookItem from './BookItem.vue'

export default {
  name: 'BookList',
  components: { BookItem },
  data() {
    return {
      books: [
        { id: 1, name: '高等数学', price: 99.6, count: 1, isEditing: false },
        { id: 2, name: '线性代数', price: 26.8, count: 1, isEditing: false },
        { id: 3, name: '大学物理', price: 26.3, count: 1, isEditing: false },
        { id: 4, name: 'Python学习', price: 49.9, count: 1, isEditing: false }
      ],
      currentIndex: -1,
      showAddButton: true,
    }
  },
  computed: {
    totalPrice() {
      return this.books.reduce((total, book) => total + book.price * book.count, 0)
    },
    selectedBookName() {
      return this.currentIndex !== -1 ? this.books[this.currentIndex].name : ''
    }
  },
  methods: {
    formatPrice(price) {
      return '¥' + price.toFixed(2)
    },
    handleSelect(index) {
      this.currentIndex = index
    },
    handleUpdate(updatedBook) {
      this.books.splice(updatedBook.index, 1, updatedBook.book)
    },
    handleRemove(index) {
      this.books.splice(index, 1)
      if (this.currentIndex === index) {
        this.currentIndex = -1
      } else if (this.currentIndex > index) {
        this.currentIndex--
      }
    },
    addBook() {
      const newId = this.books.length > 0 ? Math.max(...this.books.map(b => b.id)) + 1 : 1
      this.books.push({
        id: newId,
        name: '',
        price: 0,
        count: 1,
        isEditing: true
      })
      this.currentIndex = this.books.length - 1
      this.showAddButton = false
    },
    confirmAdd() {
      const newBook = this.books[this.books.length - 1]
      if (newBook.name.trim() && !isNaN(newBook.price) && newBook.price > 0) {
        newBook.isEditing = false
        this.showAddButton = true
      } else {
        alert('请正确填写书籍信息')
      }
    },
    cancelAdd() {
      this.books.pop()
      this.currentIndex = -1
      this.showAddButton = true
    }
  }
}
</script>