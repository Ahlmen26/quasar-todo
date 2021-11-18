<template>
  <q-page class="bg-grey-3 column">
    <q-list
      class="bg-white"
      separator
      bordered>
      
      <q-item
        v-for="task in tasks"
        :key="task.title"
        @click="task.done = !task.done"
        clickable
        :class="{ 'done': task.done }"
        v-ripple
      >
        <q-item-section avatar>
          <q-checkbox
            v-model="task.done"
            class="no-pointer-events"
            color="primary" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>
      </q-item>

    </q-list>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue';

export default defineComponent({
  data() {
    return {
      tasks: [
        { title: 'Get money', done: false },
        { title: 'Budget money', done: true },
        { title: 'Work for money', done: false },
      ],
    }
  }
})
</script>
<style lang="scss">
  .done {
    .q-item__label {
      text-decoration: line-through;
      color: #bbb;
    }
  }
</style>
