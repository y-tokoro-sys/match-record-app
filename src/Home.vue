<template>
  <div>
    <h1>対戦記録一覧</h1>
    <MatchTable :matches="matches" @edit="emit('edit', $event)" />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import MatchTable from './components/MatchTable.vue'

const matches = ref([])

// App.vue にイベントを渡す
const emit = defineEmits(['edit'])

onMounted(async () => {
  const res = await fetch('http://localhost:3000/matches')
  matches.value = await res.json()
})
</script>
