<template>
  <div v-if="isPending">Loading..</div>
  <div v-else-if="data.length">
    <table class="table">
      <thead>
        <tr>
          <th>User ID</th>
          <th>ID</th>
          <th>Title</th>
          <th>Completed</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(d, i) in data" v-bind:key="i">
          <td>{{ d.userId }}</td>
          <td>{{ d.id }}</td>
          <td>{{ d.title }}</td>
          <td>{{ d.completed }}</td>
        </tr>
      </tbody>
    </table>
  </div>
  <div v-else-if="error">Something went wrong {{ error }}</div>
</template>

<script>
import { ref, watchEffect } from "vue";

function useFetch(getUrl) {
  const data = ref([]);
  const error = ref(null);
  const isPending = ref(true);

  watchEffect(() => {
    isPending.value = true;
    error.value = null;
    fetch(getUrl())
      .then((resp) => resp.json())
      .then((_data) => {
        data.value.push(_data);
        isPending.value = false;
      })
      .catch((_error) => {
        error.value = _error.message;
      });
  });
  return {
    data,
    error,
    isPending,
  };
}

export default {
  name: "Generator",
  props: ["id"],
  setup(props) {
    console.log(props);
    const { data, error, isPending } = useFetch(
      () => `https://jsonplaceholder.typicode.com/todos/${props.id}`
    );

    return {
      data,
      error,
      isPending,
    };
  },
};
</script>

<style scoped>
.card {
  height: 100%;
}
label {
  font-size: 20px;
}
a {
  word-break: break-word;
}
</style>
