<template>
	<modal :name="nameModal" :height="heightModal" :width="widthModal">
		<h4> Paste image clipboard</h4>
		<h5>Press CTRL + V</h5>
		
		<img :src="blobImage">
	
	</modal>
</template>

<script>
import Vue from 'vue'
import modal from 'vue-js-modal'
Vue.use(modal)
export default {
	props: {
		height: String,
		width: String,
		name: String
	},
	data:() => ({
		nameModal: "Clipboard",
		heightModal: "380",
		widthModal: "600",
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
				const data = await navigator.clipboard.read()
				const clipboardContent = data[0];
				const types = clipboardContent.types[0]
				
				if(types === 'image/png') {
					const blob = await clipboardContent.getType('image/png');
					this.blobImage = window.URL.createObjectURL(blob);

				}

				sum = 0;
				this.keyControl = 0;
				this.keyV = 0;
			}

		}


	},

	mounted() {
		document.addEventListener('keyup', this.getKeyPress)
	}

}
</script>

<style>

</style>