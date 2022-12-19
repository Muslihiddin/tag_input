<script setup>
import { reactive } from "vue";

const tags = reactive(["first"]);

const deleteCurrent = (index) => tags.splice(index, 1);

const addTag = (event) => {
  if (event.target.value.length == 0 && event.code == "Backspace") {
    tags.splice(tags.length - 1, 1);
  }

  if (event.code === "Comma" || event.code === "Enter") {
    let val = event.target.value.trim();
    if (val.length > 0) {
      tags.push(val);
      event.target.value = "";
    }
  }
};
</script>
<template>
  <div class="container mx-auto px-[4rem] py-[2rem] flex items-center gap-2">
    <TransitionGroup
      name="tagsList"
      tag="ul"
      class="flex items-center gap-2 flex-wrap"
    >
      <li
        class="bg-slate-100 rounded px-2 flex items-center gap-x-1"
        v-for="(item, index) in tags"
        :key="item"
      >
        <span
          class="text-gray-400 cursor-pointer hover:text-black"
          @click="deleteCurrent(index)"
          >x</span
        >
        {{ item }}
      </li>
    </TransitionGroup>
    <input
      type="text"
      placeholder="Enter a tag"
      @keydown="addTag"
      class="p-1"
    />
  </div>
</template>
<style>
.tagsList-enter-active,
.tagsList-leave-active {
  transition: all 0.5s ease;
}
.tagsList-enter-from,
.tagsList-leave-to {
  opacity: 0;
  transform: translateY(-30px);
}
</style>
