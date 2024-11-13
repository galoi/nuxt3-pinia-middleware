<script lang="ts">
import { defineNuxtComponent } from 'nuxt/app';

definePageMeta({
  middleware: [
    () => {
      console.log('middleware!!!')

      const counterStore = useCounterStore()

      console.log('middleware before increment', counterStore.count)

      counterStore.increment()

      console.log('middleware after increment', counterStore.count)
    }
  ]
})

export default defineNuxtComponent({
  computed: {
    counterStore() {
      console.log('computed')
      return useCounterStore()
    },
    count() {
      return this.counterStore.count
    },
  },

  methods: {
    increment() {
      this.counterStore.increment()
    },

    decrement() {
      this.counterStore.decrement()
    },
  },

  created() {
    console.log('created')
  },
})
</script>

<template>
  <div>
    <p>カウント: {{ count }}</p>
    <p>ページ遷移時に 1 増えます</p>
    <button @click="increment">増やす</button>
    <button @click="decrement">減らす</button>
    <div style="margin-top: 10px">
      <NuxtLink to="/test">test へ</NuxtLink>
    </div>
  </div>
</template>
