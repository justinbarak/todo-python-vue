<!-- ListView.vue -->

<script setup>
import { ref, computed } from 'vue'

const props = defineProps(['listData', 'activeListName'])
const emit = defineEmits(['update:listData'])

const activeListItems = computed(() => {
  return (props.listData.find(element => element.name == props.activeListName)).items;
});


function clickedItem(event, item) {
  // console.log(event)
  console.log(item)
  console.log(activeListItems.value)
  const i = activeListItems.value.indexOf(item);
  if (i > 0) {
    emit('update:listData', props.listData.map(obj => {
      if (obj.name === props.activeListName) {
        return { ...obj, items: activeListItems.value.splice(i, i) };
      } else {
        return obj;
      }
    }));
  } else {
    console.log('bad value selected...');
  }
}
</script>

<template>
  <div class="">
    <div v-for="item in activeListItems">
      <div class="form-control text-lg shadow" @click="clickedItem($event, item)">
        <label class="label cursor-pointer px-8">
          <input type="checkbox checkbox-primary" checked="unchecked" class="checkbox" />
          <span class="label-text text-left">{{ item }}</span>
        </label>

      </div>
    </div>
    <!-- Include space for readied to be added list item -->
    <div class="form-control text-lg shadow" @click="clickedItem($event, item)">
      <label class="label cursor-pointer px-8">
        <input type="checkbox checkbox-secondary" checked="unchecked" class="checkbox" />
        <span class="label-text text-left">{{ item }}</span>
      </label>

    </div>
  </div>
</template>

<style></style>