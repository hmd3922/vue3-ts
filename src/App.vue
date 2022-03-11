<template>
  <div id="nav">
    <router-link to="/">Home</router-link>|
    <router-link to="/about">About</router-link>
    <div>
      <button v-for="(item, index) in arr" :key="index" @click="changeBtn(index)">{{ index + 1 }}:{{ item }}</button>
      <div>你选择了：{{ seleA }}</div>
    </div>
  </div>
  <router-view />
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
export default defineComponent({
  name: 'App',
  setup() {
    const arr = ref(['rew', 'tre', 'op']);
    const arr1 = ref([{ name: 'rew' }, { name: 'opi' }, { name: 'opo' }]);
    const seleA = ref('');
    // const seleA = ref([{ num: 0 }, { name: "" }]);
    const changeBtn = (index: number) => {
      seleA.value = arr.value[index];
      // seleA.value.name = arr1.value[index];
    };
    return {
      arr,
      arr1,
      seleA,
      changeBtn
    };
  }
});
</script>
<style lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
