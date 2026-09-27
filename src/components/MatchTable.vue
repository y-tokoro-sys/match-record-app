<template>
  <table border="1" cellpadding="6" cellspacing="0" style="width:100%;border-collapse:collapse;">
    <thead>
      <tr>
        <th>日付</th>
        <th>時間</th>
        <th>自キャラ</th>
        <th>相手</th>
        <th>結果</th>
        <th>メモ</th>
        <th>削除</th>
        <th>編集</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="m in sorted" :key="m.id">
        <td>{{ m.date }}</td>
        <td>{{ m.time }}</td>
        <td>{{ m.player }}</td>
        <td>{{ m.enemy }}</td>
        <td>{{ m.result }}</td>
        <td>{{ m.memo }}</td>
        <td><button @click="remove(m.id)">削除</button></td>
        <td><button @click="$emit('edit', m)">編集</button></td>
      </tr>
    </tbody>
  </table>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  matches: Array
})

const sorted = computed(() => {
  return [...props.matches].sort((a, b) =>
    (b.date + b.time).localeCompare(a.date + a.time)
  )
})
async function remove(id) {
  await fetch(`http://localhost:3000/matches/${id}`, {
    method: 'DELETE'
  })
  alert('削除しました')
}
</script>
