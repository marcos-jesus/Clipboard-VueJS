<template>
	<modal :name="nameModal">
		<div class="times" @click="closeModal">
			x
		</div>
		<div style="padding-top:40px;">
			<img :src="blobImage" :width="widthImage" :height="heightImage">
		</div>
	
		<div class="send">
			<img src="https://img.icons8.com/external-kmg-design-flat-kmg-design/32/000000/external-send-user-interface-kmg-design-flat-kmg-design.png"/>
		</div>
	</modal>
</template>

<script>
import Vue from 'vue'
import modal from 'vue-js-modal'
Vue.use(modal)
export default {
	props: {
		nameModal: String,
		widthImage: String,
		heightImage: String,
	},
	data:() => ({
		blobImage: {},
		keyControl: 0,
		keyV: 0,
	}),

	methods: {
		getKeyPress(event) {
			if(event.key === "Control") {
				this.keyControl = 1;
			}

			if(event.key === "v") {
				this.keyV = 1;
			}

			this.openControl()
		},

		async openControl() {
			let sum = this.keyControl + this.keyV;

			if(sum === 2) {
				this.$modal.show(this.nameModal);
				const data = await navigator.clipboard.read();
				const clipboardContent = data[0];
				const types = clipboardContent.types[0];
				
				if(types === 'image/png') {
					const blob = await clipboardContent.getType('image/png');
					this.blobImage = window.URL.createObjectURL(blob);

				}

				sum = 0;
				this.keyControl = 0;
				this.keyV = 0;
			}

		},

		closeModal() {
			this.$modal.hide(this.nameModal);
		}

	},

	mounted() {
		document.addEventListener('keyup', this.getKeyPress);
	}

}
</script>

<style scoped>
	.times {
		display:flex;
		justify-content:flex-end;
		padding-right:10px;
		padding-top:2px;
		cursor:pointer;
		font-size:24px;
		color:red;
	}

	.send {
		display:flex;
		justify-content:flex-end;
		padding-right:10px;
		cursor:pointer;
	}
</style>