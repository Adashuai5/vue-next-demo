<template>
  <div class="test">
    <h1>test count: {{count}}</h1>
    <button @click="add">+1</button>
    <div>count * 2 = {{doubleCount}}</div>
    <div>state from vuex {{a}}</div>
    <button @click="update">update a</button>
  </div>
</template>

<script>
import { ref, computed, watch, getCurrentInstance } from "vue";

export default {
  setup() {
    const count = ref(0);

    const add = () => {
      count.value++;
    };

    watch(
      () => count.value,
      val => {
        console.log(`count is ${val}`);
      }
    );

    const doubleCount = computed(() => count.value * 2);

    const { ctx } = getCurrentInstance();
    console.log(ctx);
    console.log(ctx.$router.currentRoute.value);

    const a = computed(() => ctx.$store.state.test.a);
    const update = () => {
      ctx.$store.commit("setTestA", count);
    };

    return {
      count,
      add,
      doubleCount,
      a,
      update
    };
  }
};
</script>

<style scoped>
.test {
  color: red;
}
</style>