<template>
  <div class="app">
      <div class="formLayout">
        <addgoods
          @setPost="setPost"
        />
      </div>
      <div class="postsLayout">
        <posts-component
          :posts="sortedPosts"
          @remove="removePost"
        />
      </div>
      <div class="selectLayout">
        <my-select
          v-model="selectedSort"
          :options="sortOptions"
          @changeOption="changeOption"
        />
      </div>
    </div>
</template>

<script setup>
import { computed, ref } from 'vue'

const posts = ref([])
const sortOptions = ref([
  {value: '', name: 'По умолчанию'},
  {value: 'name', name: 'По наименованию'},
  {value: 'min', name: 'По цене: от меньшего к большему'},
  {value: 'max', name: 'По цене: от большего к меньшему'},
])
let selectedSort = ref('')

const setPost = (post) => {
  posts.value.push(post);
}

const removePost = post => {
  posts.value = posts.value.filter(p => p.id !== post.id)
}

const changeOption = select => {
  selectedSort.value = select
}

const sortedPosts = computed (() => {
  if(selectedSort.value === 'name') {
    return [...posts.value].sort((post1, post2) => {
      console.log(post1.name?.localeCompare(post2.name))
      return post1.name?.localeCompare(post2.name)
    })
  }
  else if(selectedSort.value === 'min'){
    return [...posts.value].sort((post1, post2) => {
      post2.price = Number(post2.price)
      post1.price = Number(post1.price)
      return post1.price - post2.price
    })
    }
  else if(selectedSort.value === 'max'){

    return [...posts.value].sort((post1, post2) => {
      post2.price = Number(post2.price)
      post1.price = Number(post1.price)
      return post2.price - post1.price
    })
  }
  else {
    return [...posts.value]
  }

  }
 )

</script>

<style lang="scss">
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  background: #E5E5E5;
}
.app{
  display: flex;
}
.formLayout{

}
.selectLayout{
  position: relative;
  left: -155px;
  top: 31px;
  z-index: 2;
}
.postsLayout{
  position: relative;
  top: 77px;
  left: 80px;
  z-index: 3;
}

</style>
