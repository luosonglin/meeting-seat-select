<template>
	<div class="home">
		<el-container>
			<el-header>
				<el-image :src="logo_url" fit="contain"></el-image>
				<el-menu :default-active="activeIndex" mode="horizontal" @select="handleSelect"
					background-color="#FFFFFF" text-color="#333333" active-text-color="#333333">
					<el-menu-item index="1">选座</el-menu-item>
					<!-- <el-menu-item index="2">其他</el-menu-item> -->
				</el-menu>
			</el-header>
			<el-main>
				<SeatSelect v-if="value == 1" />
				<div v-else>
					{{value}}
				</div>
			</el-main>
			<!-- <el-footer> 松林测试 </el-footer> -->
		</el-container>
	</div>
</template>

<script>
	import SeatSelect from '../components/SeatSelect.vue'
	export default {
		name: 'home',
		components: {
			SeatSelect
		},
		data() {
			return {
				activeIndex: '1',
				value: '1',
				logo_url: 'http://120.76.118.56:8129/img/logo.1d34e0b3.svg',
				data: []
			}
		},
		methods: {
			handleSelect(key, keyPath) {
				this.value = key
			}
		}
	}
</script>

<style>
	html,
	body,
	#app,
	.home,
	.el-container {
		height: 100%;
	}

	.el-header {
		display: flex;
		flex-direction: row;
		background-color: #FFFFFF;
		padding: 0;
		color: #333333;
		text-align: center;
		line-height: 60px;
	}

	.el-image {
		margin-left: 100px;
		margin-right: 50px;
		width: 100px;
	}

	.el-main {
		background-color: #F4F6F9;
		color: #333333;
		text-align: center;
		padding: 10px;
	}

	.el-footer {
		padding: 0;
		background-color: #D7D7D7;
		color: #333333;
		font-size: small;
		line-height: 30px;
	}
</style>
