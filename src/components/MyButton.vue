<template>
	<button @click="onClick()" :style="{ backgroundColor: color }" class="btn">
		{{ text }}
	</button>
</template>

<script>
export default {
	name: 'MyButton',
	props: {
		text: String,
		color: String,
	},

	methods: {
		onClick() {
			this.$emit('btn-click');
		},
	},
};
</script>
