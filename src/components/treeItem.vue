<template>
	<div
		:class="[
			'tree-item',
			{ hasChild: prop.children, 'is-expand': prop.children && isExpand }
		]"
		:style="{ display: type }"
		@click.stop="handleClick"
	>
		<div
			:class="
				`content ${
					collapse ? (prop.children ? 'iconfont icon-jiantou' : 'no-child') : ''
				}`
			"
		>
			<slot name="default" :data="prop"></slot>
		</div>
		<div class="child" v-if="prop.children">
			<collapse-transition>
				<div class="collapse" v-show="isExpand">
					<tree-item
						:collapse="collapse"
						v-for="item in prop.children"
						:key="item[keyProp]"
						:prop="item"
						:type="type"
					>
						<template v-slot:default="scope">
							<slot name="default" :data="scope.data"></slot>
						</template>
					</tree-item>
				</div>
			</collapse-transition>
		</div>
	</div>
</template>

<script>
import CollapseTransition from './collapse-transition';
export default {
	name: 'tree-item',
	components: { CollapseTransition },
	props: {
		prop: {
			Object
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
			String
		}
	},
	data() {
		return {
			isExpand: true
		};
	},
	methods: {
		handleClick() {
			if (!this.prop.children || !this.collapse) return;
			this.isExpand = !this.isExpand;
		}
	}
};
</script>

<style lang="less" scoped>
.tree-item:hover,
.tree-item > .hasChild > .content:hover {
	cursor: pointer;
}
.tree-item {
	display: inline-block;
	& > .content.no-child {
		margin-left: 21px;
	}
	& > .content::before {
		display: inline-block;
		margin-right: 5px;
		transition: transform 0.3s linear;
	}
	&.is-expand {
		& > .content::before {
			transform: rotate(90deg);
		}
	}
	&.hasChild,
	&.hasChild > .content {
		width: 100%;
	}
	&.hasChild > .content:hover {
		background-color: #d2d2d2;
	}
	& > .child {
		padding-left: 20px;
		box-sizing: border-box;
	}
}
</style>
