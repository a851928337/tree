<template>
  <div id="app">
    <tree width="200px" :props="list">
      <template v-slot:default="scope">
        <span>{{ scope.data.label }}</span>
      </template>
    </tree>
  </div>
</template>

<script>
import Tree from './components/tree.vue';

export default {
  name: 'App',
  components: {
    Tree,
  },
  data() {
    return {
      list: [
        {
          label: '节点1',
          children: [
            {
              label: '节点1-1',
              children: [
                {
                  label: '节点1-1-1',
                },
                 {
                  label: '节点1-1-2',
                },
                 {
                  label: '节点1-1-3',
                },
              ],
            },
             {
              label: '节点1-2',
            },
          ],
        },
        {
          label: '节点2',
        },
      ],
    };
  },
};
</script>

<style lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
