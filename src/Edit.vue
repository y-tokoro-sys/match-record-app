<template>
  <div>
    <h1>対戦記録の編集</h1>

    <form @submit.prevent="submit">
      <div>
        <label>日付</label>
        <input v-model="form.date" type="date" required />
      </div>

      <div>
        <label>時間</label>
        <input v-model="form.time" type="time" required />
      </div>

      <div>
        <label>自キャラ</label>
        <input v-model="form.player" type="text" required />
      </div>

      <div>
        <label>相手</label>
        <input v-model="form.enemy" type="text" required />
      </div>

      <div>
        <label>結果</label>
        <select v-model="form.result">
          <option value="win">win</option>
          <option value="lose">lose</option>
        </select>
      </div>

      <div>
        <label>メモ</label>
        <input v-model="form.memo" type="text" />
      </div>

      <button type="submit">更新</button>
    </form>
  </div>
</template>

<script setup>
import { reactive, watch } from 'vue'

const props = defineProps({
  match: Object
})

const form = reactive({
  date: '',
  time: '',
  player: '',
  enemy: '',
  result: 'win',
  memo: ''
})

// 編集対象が来たら初期値をセット
watch(
  () => props.match,
  (match) => {
    console.log('Edit.vue が受け取った match:', match)

    if (match) {
      Object.assign(form, match)
      console.log('コピー後のform:', form)
    }
  },
  { immediate: true }
)

async function submit() {
  await fetch(`http://localhost:3000/matches/${props.match.id}`, {
    method: 'PUT',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(form)
  })

  alert('更新しました')
}
</script>