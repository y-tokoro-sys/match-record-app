<script setup>
import { ref } from 'vue'
import Home from './Home.vue'
import New from './New.vue'
import Edit from './Edit.vue'

const page = ref('home')
const editing = ref(null)

function startEdit(m) {
  page.value = 'edit'
  editing.value = m
}


</script>

<template>
  <button @click="page = 'home'">一覧</button>
  <button @click="page = 'new'">新規登録</button>

  <Home
    v-if="page === 'home'"
    @edit="startEdit"
  />

  <New v-if="page === 'new'" />

  <!-- ★ここが重要！ -->
   <Edit v-if="page === 'edit'" :match="editing" />

</template>
