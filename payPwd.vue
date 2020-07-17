<template>
	<div class="code-input-main">
		<div @click="getFocus" class="code-input-main-item" v-for="(item,index) in codeList" :key="index" :style="{borderRight:codeList.length==(index+1)?'1px solid rgba(213,213,213,1)':'',zIndex: 999,cursor: 'text'}">
			<span v-if="code[index]"></span>
		</div>
		<input ref='codeInput' class="code-input-input" autocomplete="off" v-model="code" :maxLength="6" />
	</div>
</template>

<script>
	export default {
		name: "CodeInput",
		data() {
			return {
				codeList: [],
				code: ''
			};
		},
		mounted() {
			this.codeList = new Array(6).fill("");
		},
		watch: {
			code() {
				if (this.code.length > this.codeLength) {
					this.code = this.code.substring(0, this.codeLength);
				}
				this.$emit('getPwd', this.code)
			}
		},
		methods: {
			getFocus() {
				this.$refs.codeInput.focus()
			}
		}
	};
</script>
<style scoped>
	input::-webkit-outer-spin-button,
	input::-webkit-inner-spin-button {
		-webkit-appearance: none !important;
		margin: 0;
	}

	.code-input-main {
		width: 216px;
		display: flex;
		flex-direction: row;
		justify-content: space-around;
		position: relative;
	}

	.code-input-input {
		height: 36px;
		width: 100%;
		position: absolute;
		border: none;
		outline: none;
		color: transparent;
		background-color: transparent;
		text-shadow: 0 0 0 transparent;
	}

	.code-input-main-item {
		background: #fff;
		width: 36px;
		height: 36px;
		display: flex;
		justify-content: center;
		align-items: center;
		border: 1px solid rgba(213, 213, 213, 1);
		border-right: none;
		font-size: 30px;
		color: black;
	}

	.code-input-main-item span {
		height: 8px;
		width: 8px;
		background: #000000;
		border-radius: 100%
	}
</style>
