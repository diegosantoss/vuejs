<template>
	<section id="counter">
		<h1>{{ this.count.msg }}</h1>
		<button v-on:click="handleDecItem">-</button>
		<p>{{ this.count.value }}</p>
		<button v-on:click="handleIncItem">+</button>
	</section>     
</template>

<script>
	export default {
		name: 'Counter',
		props: {
			count: {
				type: Object
			}
		},
		methods: {
			handleIncItem: function(){
				this.$emit('handleInc');
			},
			handleDecItem: function(){
				this.$emit('handleDec');
			}
		}
	}
</script>

<style>
	#counter{
		display: flex;
		flex-direction: row;
		align-items: center;
		flex-wrap: wrap;
		justify-content: center;
		font-family: 'Trebuchet MS';
	}

	#counter h1{
		display: block;
		width: 100%;
		font-family: 'Trebuchet MS';
	}

	#counter p{
		font-size: 25px;
		margin: 0 20px;
	}

	#counter button{
		padding: 3px 15px;
		font-size: 20px;
	}
</style>