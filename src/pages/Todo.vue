<template>
  <q-page class="bg-grey-3 column">
    <div class="row q-pa-sm bg-primary">
      
      <q-input
        class="col"
        square
        filled
        bg-color="white"
        dense
        v-model="newTask"
        placeholder="Add Task">
          <template v-slot:append>
            <q-btn @click="addTask" round dense flat icon="add"></q-btn>
          </template>

      </q-input>
        
    </div>

    <q-list
      class="bg-white"
      separator
      bordered>
      
      <q-item
        v-for="(task, index) in tasks"
        :key="task.title"
        @click="task.done = !task.done"
        clickable
        :class="{ 'done bg-green-1': task.done }"
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

        <q-item-section
          side
          v-if="task.done"
        >
          <q-btn
              @click.stop="deleteTask(index)"
              round
              flat
              dense
              color="red"
              icon="delete" />

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
      newTask: '',
      tasks: [
        { title: 'Get money', done: false },
        { title: 'Budget money', done: false },
        { title: 'Work for money', done: false },
      ],
    }
  },
  methods: {
    addTask() {
      this.tasks.push({title: this.newTask, done: false})
    },
    deleteTask(index) {

      this.$q.dialog({
        title: 'Confirm',
        message: 'Are you sure you want to delete?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.tasks.splice(index, 1)

        this.$q.notify({
          color: 'green',
          position: 'bottom-right',
          message: 'Task deleted',
          icon: 'check_circle'
        })
      })

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
