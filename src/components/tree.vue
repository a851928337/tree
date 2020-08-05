<template>
  <div class="tree" :style="{ width }">
    <tree-item
      v-for="(item, index) in props"
      :key="item.label + index"
      :prop="item"
    >
      <template v-slot:default="scope">
        <slot :data="scope.data"></slot>
      </template>
    </tree-item>
  </div>
</template>

<script>
import TreeItem from './treeItem';
export default {
  name: 'tree',
  components: { TreeItem },
  props: {
    props: {
      Object,
    },
    width: {
      String,
    },
  },
};
</script>

<style lang="less" scoped>
.tree {
  text-align: left;
  display: inline-block;
}
</style>
