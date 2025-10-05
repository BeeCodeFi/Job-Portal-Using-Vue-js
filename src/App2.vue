<script>
export default {
  data() {
    return {
      name: 'John Doe',
      status: 'active',
      tasks: ['Task 1', 'Task 2', 'Task 3'],
      link: 'https://www.google.com',
    };
  },
  methods:{
    ToggleEvent(){
      this.status = this.status === 'active' ? 'inactive' : 'active';
      console.log('Chnaged Status');
    },
  }
};
</script>

<template>
  <h1>
    {{ name }}
  </h1>
  <p v-if="status === 'active'">
    Status is active  
  </p>
  <p v-else-if="status === 'inactive'">
    Status is inactive
  </p>
  <p v-else>
    Status is unknown
  </p>
  <h3>
    Tasks:
  </h3>
    <ul>
      <li v-for="task in tasks" key="task">{{ task }}</li>
    </ul>
    <a :href="link" target="_blank">Click for Google</a>
    &nbsp;
    <button @click="ToggleEvent">Change Status</button>
</template>

