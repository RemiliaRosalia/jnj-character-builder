<template>
    HelloWorld
  <button @click="saveFile">Save Character</button>
  <button @click="loadFile">Load Character</button>
</template>

<script>
import Builder from './Builder.vue'
export default 
{
    //props: ['primColor'],
    methods:
    {
        saveFile()
        {

        },
        loadFile()
        {

        }
    },
    components:
    {
        Builder
    }
}
</script>

<style>

</style>