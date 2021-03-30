<template>
  <div class="container" @scroll="handleScroll" ref="container">
    <div class="item-wrap" ref="itemWrap">
      <Item v-for="item in showData" :item="item" />
    </div>
    <div class="scroll" ref="scroll"></div>
  </div>
</template>

<script setup>
  import { ref, onMounted, reactive, computed } from "vue"
  import Item from "./Item.vue"

  const props = defineProps({
    data: Array
  })
  const state = reactive({
    itemHeight: 50,
    startIndex: 0,
    showNum: 10
  })
  const showData = computed(() => {
    return props.data.slice(state.startIndex, state.startIndex + 10)
  })
  const itemWrap = ref(null)
  const container = ref(null)
  const scroll = ref(null)
  onMounted(() => {
    itemWrap.value.style.height = state.showNum * state.itemHeight + "px"
    scroll.value.style.height = props.data.length * state.itemHeight + "px"
  })

  function handleScroll(e) {
    state.startIndex = container.value.scrollTop / state.itemHeight
    // debugger
    itemWrap.value.style.top = container.value.scrollTop + "px"
    // console.log(container.value.scrollTop);
    // debugger 
  }
</script>

<style scoped>
  .container {
    width: 300px;
    height: 500px;
    overflow-y: scroll;
    position: relative;
  }

  .item-wrap {
    width: 100%;
    position: absolute;
    top: 0;
  }

  .scroll {
    width: 100%;
  }
</style>