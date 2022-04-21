<template>
    <div>
        <button @click="getLorem">lorem ipsum</button>
        <p>{{ lorem.length != 0 ? lorem : "load Lorem Ipsum" }}</p>
    </div>

</template>

<script setup>
import axios from "axios";
import { Container, Draggable } from 'vue3-smooth-dnd';
import { onBeforeMount, ref } from "vue";


let lorem = ref("");

onBeforeMount(() =>{
    getLorem();
})

async function getLorem() {
  const response = await axios.get("http://digico-kanban.tk:9000/test/hello");
  console.log(response.data);
  lorem.value = response.data;
}

// mock
const scene = {
  type: 'container',
  props: {
    orientation: 'horizontal'
  },
  children: generateItems(1, i => ({
    id: `column${i}`,
    type: 'container',
    name: generateWords(Math.random() * 2 + 1),
    props: {
      orientation: 'vertical',
    },
    children: generateItems(+(Math.random() * 10).toFixed() + 5, j => ({
      type: 'draggable',
      id: `${i}${j}`,
      loading: false,
      data: generateWords(Math.random() * 12 + 2)
    }))
  }))
}

const onCardDrop = (columnId, dropResult) => {

}

const generateWords = (n) => {

}

const generateItems = (count, creator) => {
    const items = []
    for (let i = 0; i < count; i++) {
        items.push(creator(i))
    }
    return items
}

</script>

<style>

</style>
