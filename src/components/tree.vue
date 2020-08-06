<template>
	<div class="tree" :style="{ width }">
		<tree-item
			:collapse="collapse"
			v-for="item in props"
			:key="item[keyProp]"
			:prop="item"
			:type="type"
		>
			<template v-slot:default="scope">
				<slot :data="scope.data"></slot>
			</template>
		</tree-item>
	</div>
</template>

<script>
import TreeItem from './treeItem';
import './collapse-transition.css';
import './common.css';
export default {
	name: 'tree',
	components: { TreeItem },
	props: {
		props: {
			Object
		},
		width: {
			String
		},
		keyProp: {
			type: String,
			default: 'id'
		},
		collapse: {
			type: Boolean,
			default: true
		},
		type: {
			type: String,
			default: 'inline-block'
		}
	}
};
</script>

<style lang="less" scoped>
.tree {
	text-align: left;
	display: inline-block;
	user-select: none;
}
</style>
