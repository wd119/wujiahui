<template>
<div class="song-list">
<div class="list-header">
<img :src="list.coverImgUrl" :alt="list.name" class="list-cover">
<div class="list-info">
<h3>{{list.name}}</h3>
<p class="description">{{list.description}}</p>
</div>
<ul class="track-list">
    <li v-for="(track,index) in list.tracks" :key="index" class="track-item">
      <span class="track-index">{{index+1}}</span>
      <img :src="track.picUrl" :alt="track.name" class="track-img">
      <span class="track-name">{{track.name}}</span>
    </li>
</ul>
</div>
</div>
</template>
<script>
export default{
    name: "List",
    props:{
        list: {
            type: Object,
            required: true
        }
    }
}
</script>
<style scoped>
.song-list{
    background:#fff;
    border-radius: 5px;
    padding: 15px;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}
.list-cover{
    width:80px;
    height:80px;
    border-radius: 5px;
    object-fit: cover;
    margin-right:15px;
}
.list-info h3 {
  font-size: 18px;
  margin-bottom: 8px;
  color: #333;
}
.description {
  font-size: 12px;
  color: #999;
  line-height: 1.4;
}
.track-list {
  list-style: none;
}
.track-item {
  display: flex;
  align-items: center;
  padding: 8px 0;
  border-bottom: 1px solid #f0f0f0;
}
.track-index {
  width: 20px;
  text-align: center;
  color: #999;
  font-size: 14px;
  margin-right: 10px;
}
.track-img {
  width: 40px;
  height: 40px;
  border-radius: 4px;
  object-fit: cover;
  margin-right: 10px;
}

.track-name {
  font-size: 14px;
  flex: 1;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
</style>