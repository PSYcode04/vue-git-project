<template>
  <div>
    <span>D & D</span>
    <hr/>
    <Container class="p-8" @drop="onDrop">
        <Draggable style="height: 50px; border: 1px solid; margin: 20px; background-color:#FFFFCC;" v-for="(item, i) in items" :key="item.id">
          <div>
            {{i + 1}} -> {{item.data}}
          </div>
        </Draggable>
        <br>
        <hr/>
    </Container>
  </div>
</template>

<script>
import { Container, Draggable } from "vue3-smooth-dnd";
export default {
  name: "app",
  components: { Container, Draggable },
  data() {
    return {
      items: [
        { id: 1, data: "TEST 1" },
        { id: 2, data: "TEST 2" },
        { id: 3, data: "TEST 3" },
        { id: 4, data: "TEST 4" },
        { id: 5, data: "TEST 5" },
        { id: 6, data: "TEST 6" },
        { id: 7, data: "TEST 7" },
        { id: 8, data: "TEST 8" },
        { id: 9, data: "TEST 9" },
      ]
    };
  },
  methods: {
    onDrop(dropResult){
      this.items = this.applyDrag(this.items, dropResult);
    },
    applyDrag(arr, dragResult){
      const { removedIndex, addedIndex, payload } = dragResult;
      console.log(dragResult);
      if (removedIndex === null && addedIndex === null) return arr;
      const result = [...arr];
      let itemToAdd = payload;

      if (removedIndex !== null) {
        itemToAdd = result.splice(removedIndex, 1)[0];
      }
      if (addedIndex !== null) {
        result.splice(addedIndex, 0, itemToAdd);
      }
      return result;
    }
  }
}
</script>
