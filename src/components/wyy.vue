<template>
  <div class="home">
    <HeaderSection title="热门歌手"></HeaderSection>
    <CardList :items="artists" :cols="6">
      <template v-slot:default="{ item }">
        <div class="artist-card">
         <img :src="item.picUrl" :alt="item.name" class="artist-img">
         <p class="artist-name">{{ item.name }}</p>
        </div>

      </template>
    </CardList>
    <HeaderSection title="榜单"></HeaderSection>
    <div class="list">
      <List :list="hotSong"></List>
      <List :list="newSong"></List>
      <List :list="originSong"></List>
    </div>
  </div>
</template>
<script>
import HeaderSection from './HeaderSection'
import CardList from './cardList'
import artists from '@/data/artist'
import List from './list'
import hotSong from '@/data/hotSong'
import newSong from '@/data/newSong'
import originSong from '@/data/originSong'
export default {
  name: 'Home',
  components: {
    HeaderSection,
    CardList,
    List,
    CardList
  },
  data(){
    return {
      artists,
      hotSong,
      newSong,
      originSong

    }
  }
}
</script>
<style scoped>
.home {
  padding: 20px 0;
}

.artist-card {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin-bottom: 15px;
}

.artist-img {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  object-fit: cover;
  margin-bottom: 8px;
}

.artist-name {
  font-size: 14px;
  color: #333;
}
.list{
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
  margin-top: 20px;
}
</style>
