<template>
    <div class="card-list">
        <ul class="card-list-container">
            <li v-for="(item,index) in items" :key="index">
                <slot :item="item"></slot>
            </li>
        </ul>
    </div>
</template>
<script>
export default{
    name: "cardList",
    props:{
        items:{
            type:Array,
            required:true
        },
        cols: {
      type: Number,
      default: 5
    }
    }
}
</script>
<style scoped>
.card-list {
    width: 100%;
    margin:10px 0}
.card-list-container {
  overflow: hidden;
  margin: 0 -10px;
  display: flex;
  flex-wrap: wrap;
  list-style: none;
}

.card-list:hover {
  transform: translateY(-5px);
}

</style>
