<template>
	<div id="app">
		<tree :collapse="false" type="block" width="300px" key-prop="id" :props="list">
			<template v-slot:default="scope">
				<label @click.stop>
					<input
						@click.stop="handleClick(scope.data)"
						type="checkbox"
						v-model="scope.data.check"
					/>
					<span>{{ scope.data.label }}</span>
				</label>
			</template>
		</tree>
	</div>
</template>

<script>
import Tree from './components/tree.vue';

export default {
	name: 'App',
	components: {
		Tree
	},
	data() {
		return {
			list: [
				{
					id: 1,
					label: '节点1',
					check: false,
					children: [
						{
							id: 2,
							label: '节点1-1',
							check: false,
							children: [
								{
									id: 3,
									label: '节点1-1-1',
									check: false
								},
								{
									id: 4,
									label: '节点1-1-2',
									check: false
								},
								{
									id: 5,
									label: '节点1-1-3',
									check: false,
									children: [
										{
											id: 6,
											label: '节点1-1-3-1',
											check: false
										},
										{
											id: 7,
											label: '节点1-1-3-2',
											check: false
										}
									]
								}
							]
						},
						{
							id: 8,
							label: '节点1-2',
							check: false
						}
					]
				},
				{
					id: 9,
					label: '节点2',
					check: false
				}
			],
			checkeds: []
		};
	},
	methods: {
		handleClick(prop) {
			let nc = JSON.parse(JSON.stringify(this.checkeds));
			let objs = [prop.id];
			if (prop.children) {
				let child = JSON.stringify(prop.children);
				if (prop.check) {
					child = child.replace(/"check":true/g, '"check":false');
					child.match(/"id":\d/g).forEach((item) => {
						objs.push(Number(item.split(':')[1]));
					});
				} else {
					child = child.replace(/"check":false/g, '"check":true');
					child.match(/"id":\d/g).forEach((item) => {
						objs.push(Number(item.split(':')[1]));
					});
				}
				prop.children = JSON.parse(child);
			}
			if (prop.check) {
				const set = new Set(objs);
				let na = nc.filter((item) => {
					return !set.has(item);
				});
				this.checkeds = na;
			} else {
				this.checkeds = Array.from(new Set([...nc, ...objs]));
			}
		}
	},
	watch: {
		checkeds(n) {
			console.log(n);
		}
	}
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
