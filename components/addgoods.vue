<template>
<div class="">

    <h1 class="title">Добавление товара</h1>
    <div class="addformWrapper">
      <div class="nameWrapper">
        <div class="titleofnameWrapper">
          <p class="titleofname">Наименование товара</p>
        </div>
        <div class="inputofnameWrapper">
          <input
            v-model="post.name"
            placeholder="Введите наимениование товара"
            class="inputofname"
            :class="{redinput: nameBroked}"
          />
        </div>
        <div v-show="nameBroked" class="somethingBroked">Это поле является обязательным</div>
      </div>
      <div class="nameWrapper">
        <div class="titleofnameWrapper">
          <p class="titleofdesc">Описание товара</p>
        </div>
        <div class="inputofnameWrapper">
          <textarea v-model="post.body" placeholder="Введите описание товара" class="inputofdesc"/>
        </div>
      </div>
      <div class="nameWrapper">
        <div class="titleofnameWrapper">
          <p class="titleofname">Ссылка на изображение товаров</p>
        </div>
        <div class="inputofnameWrapper">
          <input
            v-model="post.img"
            placeholder="Введите ссылку"
            class="inputofname"
            :class="{redinput: srcBroked}"
          />
        </div>
        <div v-show="srcBroked" class="somethingBroked">Это поле является обязательным</div>
      </div>
      <div class="nameWrapper">
        <div class="titleofnameWrapper">
          <p class="titleofname">Цена товара</p>
        </div>
        <div class="inputofnameWrapper">
          <input v-model="post.price"
                 type="number"
                 placeholder="Введите цену"
                 class="inputofname"
                 :class="{redinput: priceBroked}"
          />
        </div>
        <div v-show="priceBroked" class="somethingBroked">Это поле является обязательным</div>
      </div>
      <div class="btnWrapper">
        <button @click="createPost" class="btn" :class="{succbtn: succbtn}">Добавить товар</button>
      </div>
    </div>
</div>
</template>

<script setup>
import { watchEffect, ref } from 'vue'

  const emit = defineEmits(['changeofName', 'setPost'])
  const post = ref({
    id: 0,
    name: '',
    body: '',
    img: '',
    price: '',
  })
  const nameBroked = ref(false)
  const srcBroked = ref(false)
  const priceBroked = ref(false)
  const succbtn = ref(false)

  const createPost = () => {
    post.value.id = Date.now()
    if(succbtn.value)
    {
      emit('setPost', post.value)
      post.value = {
        id: 0,
        name: '',
        body: '',
        img: '',
        price: '',
      }
    }

  }
  watchEffect(() => {
    post.value.name === '' ?  nameBroked.value = true : nameBroked.value = false;
    !post.value.img.includes('http' && '://') ? srcBroked.value = true : srcBroked.value = false;
    post.value.price === '' ? priceBroked.value = true : priceBroked.value = false

    if(!nameBroked.value && !srcBroked.value && !priceBroked.value){
      succbtn.value = true
    }
    if(nameBroked.value || srcBroked.value || priceBroked.value){
      succbtn.value = false
    }
  })

</script>
<script>
export default {
  name: "addgoods"
}
</script>

<style lang="scss" scoped>
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
}
input[type='number'] {
  -moz-appearance: textfield;
}
@import url('https://fonts.googleapis.com/css2?family=Lato&family=PT+Sans:ital,wght@0,400;0,700;1,400&family=Source+Sans+Pro:wght@400;600&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Lato&family=PT+Sans:ital,wght@0,400;0,700;1,400&family=Source+Sans+Pro:wght@400;600&display=swap');
@mixin input($h){
  background: #FFFEFB;
  font-family: 'Source Sans Pro';
  font-style: normal;
  font-weight: 400;
  font-size: 12px;
  line-height: 15px;
  color: #3F3F3F;
  border: none;
  padding: 10px 15px;
  width: 100%;
  height: $h;
}
@mixin title(){
  font-family: 'Source Sans Pro';
  font-style: normal;
  font-weight: 400;
  font-size: 10px;
  line-height: 13px;
  background-color: #FFFEFB;
  letter-spacing: -0.02em;
  color: #49485E;
}
.title{
  position: relative;
  margin-bottom: 0px;
  left: 32px;
  top: 32px;

  font-family: 'Source Sans Pro';
  font-style: normal;
  font-weight: 600;
  font-size: 28px;
  line-height: 35px;

  color: #3F3F3F;
}

.addformWrapper{
  position: relative;
  width: 332px;
  height: 440px;
  left: 32px;
  top: 42px;
  background: #FFFEFB;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  padding: 24px;
}
.nameWrapper{
  background-color: #FFFEFB;
  margin-top: 15px;
}
.nameWrapper:nth-child(1){
  margin-top: 0;
}
.titleofnameWrapper{

}
.titleofname{
  @include title
}
.titleofdesc{
  @include title
}
.titleofname::after{
  content: '\002A';
  color: #FF8484;
}
.inputofnameWrapper{
  margin-top: 5px;
  background: #FFFEFB;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
}
.inputofname{
  @include input(100%);
}
.redinput{
  @include input(100%);
  border: 1px solid #FF8484;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
}
.inputofdesc{
  @include input(108px);
  resize: none;
}
::placeholder {
  font-family: 'Source Sans Pro';
  font-style: normal;
  font-weight: 400;
  font-size: 12px;
  line-height: 15px;
  color: #B4B4B4;
}
.btnWrapper{
  background-color: #FFFEFB;
  margin-top: 23px;
}
@mixin btns($bg, $c){
  width: 284px;
  height: 36px;
  background: $bg;
  border-radius: 10px;
  font-family: 'Inter';
  font-style: normal;
  font-weight: 600;
  font-size: 12px;
  line-height: 15px;
  border: none;
  text-align: center;
  letter-spacing: -0.02em;
  color: $c;
  cursor: pointer;
}
.btn{
  @include btns(#EEEEEE, #B4B4B4)
}
.succbtn{
  @include btns(#7BAE73, #FFFFFF)
}
.somethingBroked{
  position: absolute;
  margin-top: 5px;
  background-color: #FFFEFB;
  font-family: 'Source Sans Pro';
  font-style: normal;
  font-weight: 400;
  font-size: 8px;
  line-height: 10px;
  letter-spacing: -0.02em;

  color: #FF8484;
}

</style>
