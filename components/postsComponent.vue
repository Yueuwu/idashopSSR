<template>
  <div class="postsWrapper">
    <transition-group name="list-complete">
    <post-item
      v-for="post in posts"
      :post="post"
      :key="post.id"
      @remove="$emit('remove', post)"
      class="list-complete-item"
    />
    </transition-group>

  </div>
</template>
<script setup>
const props = defineProps({
  posts: {
    type: Array
  },
})
</script>
<script>

export default {
  name: "postsComponent",

}
</script>

<style scoped>
.postsWrapper{
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  width: 1100px;
}
.list-complete-item {
  transition: all 1s;
  display: inline-block;
  margin-right: 10px;
}
.list-complete-enter, .list-complete-leave-to{
  opacity: 0;
  transform: translateY(45px);
}
.list-complete-leave-active {
  position: absolute;
}
</style>
