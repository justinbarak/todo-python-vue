<!-- ListsHeader.vue -->
<script setup>
import { ref, reactive, computed } from 'vue'

const props = defineProps(['listData', 'activeListName'])
const emit = defineEmits(['update:activeListName'])

const to_do_lists = computed(() => {
  var names = Array();
  (props.listData).forEach(element => {
    names.push(element.name)
  });
  return names
});
const activeListStyling = 'tab tab-lifted tab-active';
const inactiveListStyling = 'tab tab-lifted';

</script>

<template>
  <div class="tabs shadow-md">
    <div v-for="list_name in to_do_lists" :key="list_name.list_id" class="text-2xl">
      <div :class="[list_name == props.activeListName ? `${activeListStyling}` : `${inactiveListStyling}`]"
        @click="$emit('update:activeListName', $event.target.innerHTML)">
        {{ list_name }}
      </div>
    </div>
  </div>
</template>