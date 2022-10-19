<template>
  <q-page class="q-pa-md">
    <div class="row justify-center">
      <div class="col-xs-12 col-sm-6 col-md-4">
        <q-input rounded bottom-slots v-model="text" label="Input Todo">
          <template v-slot:prepend>
            <q-icon name="note" />
          </template>
          <template v-slot:append>
            <q-icon name="add" @click="onClickAdd" class="cursor-pointer" />
          </template>

          <template v-slot:hint>
            Ketikan Todo kamu di input ini ya...
          </template>
        </q-input>
      </div>
    </div>
    <div class="row justify-center q-mt-md">
      <div class="col-xs-12 col-sm-6 col-md-4">
        <q-list v-if="todos.length === 0" bordered padding >
          <q-item>
            <q-item-section>
              <q-item-label>Belum Ada Todo</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
        <q-list v-if="todos.length !== 0" padding>
          <div v-for="todo, i in todos" :key="i">
            <q-item :class="todo.done ? 'bg-green-2' : ''">
              <q-item-section>
                <q-item-label>{{todo.text}}</q-item-label>
                <q-item-label caption>{{todo.createDate}}</q-item-label>
              </q-item-section>
              <q-item-section side top>
                <q-btn  size="12px" color="red" flat dense round icon="delete" @click="onDelete(i)" />
                <q-btn  size="12px" color="green" flat dense round icon="done" @click="onDone(i)" />
              </q-item-section>
            </q-item>
            <q-separator />
          </div>
        </q-list>
      </div>
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'IndexPage',

  data() {
    return {
      text: '',
      todos: [],
    };
  },

  methods: {
    onClickAdd() {
      const now = Date.now();
      const createDate = new Date(now).toLocaleString();
      this.todos.push({ text: this.text, createDate, done: false });
      this.text = '';
    },
    onDelete(index) { this.todos.splice(index, 1); },
    onDone(index) { this.todos[index].done = true; },
  },

});
</script>
