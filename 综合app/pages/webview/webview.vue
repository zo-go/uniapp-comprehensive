<template>
	<web-view :src="href">

	</web-view>

</template>

<script>
	export default {
		data() {
			return {
				href: 'https://ptu.zbmwd.top/imgs/'
			}
		},
		onLoad(e) {
			console.log(e);
			this.href = this.href+e.name
		},
		methods: {
			
		}
	}
</script>

<style>

</style>
