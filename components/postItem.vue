<template>
<div class="">
  <div class="wrapper">
    <div @click="$emit('remove', post)" class="blockChild">
      <img class="removeIcon" src="https://cdn.icon-icons.com/icons2/1893/PNG/512/dustbin_120823.png" alt=""/>
    </div>
    <div class="imgWrap">
      <img class="img" :src="post.img" alt="">
    </div>
    <div class="body">
      <div class="name">{{ post.name }}</div>
      <div class="description">{{post.body}}</div>
      <div class="price">{{post.price}} руб.</div>
    </div>
  </div>
</div>
</template>

<script setup>

const props = defineProps({
  post: {
    type: Object
  }
})
</script>
<script>
export default {
  name: "postItem",
}
</script>

<style scoped>
.wrapper{
  width: 332px;
  height: 423px;
  background: #FFFEFB;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  margin-left: 16px;
  margin-bottom: 16px;
  cursor: pointer;
}
.imgWrap{
  width: 100%;
  height: 200px;
  border-radius: 4px 4px 0px 0px;
  object-fit: cover;
  text-align: center;
  background-color: #000;
}
.img{
  max-width: 100%;
  max-height: 100%;
  border-radius: 4px 4px 0px 0px;
}
.body{
  margin-top: 15px;
  background: #FFFEFB;
  padding: 0 15px;
}
.name{
  font-family: 'Source Sans Pro';
  font-style: normal;
  font-weight: 600;
  font-size: 20px;
  line-height: 25px;
  background: #FFFEFB;
  color: #3F3F3F;
  overflow: hidden;
  word-wrap: break-word;
  height: 25px;
}
.description{
  margin-top: 15px;
  font-family: 'Source Sans Pro';
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 20px;
  background: #FFFEFB;
  color: #3F3F3F;
  height: 80px;
  overflow-y: hidden;
  word-wrap: break-word
}
.price{
  margin-top: 15px;
  font-family: 'Source Sans Pro';
  font-style: normal;
  font-weight: 600;
  font-size: 24px;
  line-height: 30px;
  background: #FFFEFB;
  color: #3F3F3F;
  word-wrap: break-word
}

.wrapper .blockChild {
  display: none;
  width: 32px;
  height: 32px;
  background: #FF8484;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
}

.wrapper:hover .blockChild  {
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index:2;
  margin-left: 310px;
  margin-top: -10px;
}
.removeIcon{
  width: 15px;
  height: 15px;
  background-color: #FF8484;
  color: white;
}
</style>
