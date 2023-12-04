<script setup lang="ts">
import { getUsers, type User } from '@/model/users';
import { ref } from 'vue';

  const newTask = ref('');
  const tasks = ref([] as { id?: number, text: string, completed: boolean }[] );

  const tabList = ['Current', 'Completed', 'All'];
  const tabState = ref('Current');

  function addTask() {
    tasks.value.push({ text: newTask.value, completed: false });
    newTask.value = '';
  };

  const shouldDisplay = (task: { id?: number, text: string, completed: boolean }) =>
    (tabState.value == 'Current' && !task.completed) ||
    (tabState.value == 'Completed' && task.completed) ||
    tabState.value == 'All';

  const users = ref([] as User[] );
  getUsers().then((data) => {
    users.value = data;
  });

</script>

<template>
  <main class="columns is-multiline is-centered">
    <div class="column is-full">
      <h1 class="title is-centered" >Run With Me</h1>
      <h2 class="subtitle is-centered">
        No longer just about running!
      </h2>
      <div class="box is-centered">
        Reach your goals along side all of these other users!
      </div>
    </div>

      <div class="box" v-for="user in users" :key="user.id">
        {{ user.firstName }} {{ user.lastName }}
      </div>
  </main>
</template>
