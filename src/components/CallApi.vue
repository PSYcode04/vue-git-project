<template>
    <div>
        <button type="button" @click="getLorem">lorem ipsum</button>
        <p class="p-5">{{ lorem }}</p>
    </div>

</template>

<script setup>
import axios from "axios";
import { onBeforeMount, ref } from "vue";

let lorem = ref("");

onBeforeMount(() =>{
    getLorem();
})

const getLorem = async () => {
  const response = await axios.get("http://digico-kanban.tk:9000/test/hello");
  console.log(response.data);
  lorem.value = response.data;
};

</script>

<style scoped>
button {
    background: yellow;
}
</style>
