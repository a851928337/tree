<template>
  <div class="tree-item" @click="handleClick">
    <slot name="default" :data="prop"></slot>
    <div class="child" v-if="prop.children">
      <tree-item
        v-for="(item, index) in prop.children"
        :key="item.label + index"
        :prop="item"
      >
        <template v-slot:default="scope">
          <slot name="default" :data="scope.data"></slot>
        </template>
      </tree-item>
    </div>
  </div>
</template>

<script>
export default {
  name: 'tree-item',
  props: {
    prop: {
      Object,
    },
  },
  methods:{
    handleClick(){

    }
  }
};
</script>

<style lang="less" scoped>
.tree-item {
  display: inline-block;
  .child {
  width: 100%;
    padding-left: 20px;
    box-sizing: border-box;
  }
}
</style>
