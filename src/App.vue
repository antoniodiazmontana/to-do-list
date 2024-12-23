<template>
  <div id="app">
    <header>
      <h1>To-Do List 📝</h1>
    </header>
    <main>
      <TaskList />
    </main>
  </div>
</template>

<script>
import TaskList from "./components/TaskList.vue";

export default {
  name: "App",
  components: {
    TaskList,
  },
};
</script>

<style>
body {
  display: flex;
  flex-direction: column;
  height: 100vh;
  justify-content: center;
  align-items: center;
  margin: 0;
  font-family: "Arial", sans-serif;
  background-color: rgb(226, 214, 192);
  color: #333;
}

#app {
  width: 500px;
  border: 1px solid black;
  border-radius: 50px;
  background-color: aliceblue;
  box-shadow: 5px 5px 10px 2px grey;
}

header {
  background-color: #4caf50;
  color: white;
  padding: 20px;
  text-align: center;
  border-radius: 50px 50px 0 0;
}

main {
  padding: 20px;
  max-width: 600px;
  margin: 0 auto;
}
</style>
