<template >
    <select  class="selectC" v-model="options.value" @change="setChange">
      <option
            v-for="option in options"
            :key="option.value"
            :value="option.value"
            >
            {{ option.name }}
            </option>
    </select>
</template>

<script setup>
const props = defineProps({
    options: {
      type: Array,
      default: () => []
    }
})
const emit = defineEmits(['changeOption'])
const setChange = (event) => {
  emit('changeOption', event.target.value)
}


</script>
<script>
export default {
    name: 'my-select',
}
</script>
<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css2?family=Lato&family=PT+Sans:ital,wght@0,400;0,700;1,400&family=Source+Sans+Pro:wght@400;600&display=swap');
.selectC{
  display: inline-block;
  height: 36px;
  background: #FFFEFB;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  text-align: center;
  font-family: 'Source Sans Pro';
  font-style: normal;
  font-weight: 400;
  font-size: 12px;
  line-height: 15px;
  border: none;
  color: #737070;
}
</style>
