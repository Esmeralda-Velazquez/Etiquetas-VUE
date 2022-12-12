<script >
import ImputTag from './components/ImputTag.vue';
export default{
  components: {
    ImputTag,
  },
  methods:{
    handleOnTagsChange(tags){
      console.log(tags);
    }
  },
}
</script>

<template>
  <ImputTag :onTagsChange="handleOnTagsChange"/>
</template>

<style scoped>
</style>
