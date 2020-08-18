<template>
	<div class="home">
		<h1>Welcome to the mystery glyph reader</h1>
		<picture-input
			ref="pictureInput"
			@change="onChange"
			width="600"
			height="444"
			accept="image/jpeg, image/png"
			:removable="true"
			:customStrings="{
				upload: '<h1>Sorry!</h1>',
				drag: 'Test a glyph',
			}"
			>></picture-input
		>
	</div>
</template>

<script>
import PictureInput from 'vue-picture-input';
import * as cvstfjs from 'customvision-tfjs';
import labels from 'raw-loader!../public/models/labels.txt';

export default {
	name: 'app',
	data() {
		return {
			labels: labels,
			result: null,
			model: null,
			image: null,
			ctx: null,
		};
	},

	components: {
		PictureInput,
	},
	methods: {
		onChange(image) {
			this.ctx = this.$refs.pictureInput.$refs.previewCanvas.getContext('2d');
			this.ctx.clearRect(0, 0, this.ctx.canvas.width, this.ctx.canvas.height);

			console.log('New picture selected!');
			if (image) {
				this.predict();
			} else {
				console.log('FileReader API not supported');
			}
		},

		load(url) {
			console.log(url);
			let im = new Image();
			im.crossOrigin = 'anonymous';
			im.src = url;
			im.width = 600;
			im.height = 444;
			return im;
		},

		async predict() {
			this.image = this.load(this.$refs.pictureInput.image);

			await this.model.executeAsync(this.image).then((result) => {
				this.result = result;
				this.createBoxes();
			});
		},
		createBoxes() {
			let font = '24px helvetica';
			this.ctx.font = font;
			this.ctx.textBaseline = 'top';

			//this.ctx.clearRect(0, 0, this.ctx.canvas.width, this.ctx.canvas.height);

			let boxes = this.result[0];
			let probs = this.result[1];
			let label = this.result[2];
			let threshold = 0.01;

			this.predictions = label.map((p, i) => {
				return { index: i, label: this.labels[p] };
			});

			console.log(this.predictions);

			//only show boxes that have more than 10% probability
			let imageData = this.ctx.getImageData(0, 0, this.image.width, this.image.height);

			if (probs.some((x) => x > threshold)) {
				this.ctx.hidden = false;
				boxes.forEach((item, idx) => {
					if (probs[idx] > threshold) {
						//draw bounding boxes
						let itemclass = this.predictions[idx].label;
						let x1 = item[0] * imageData.width;
						let y1 = item[1] * imageData.height;
						let x2 = item[2] * imageData.width;
						let y2 = item[3] * imageData.height;
						this.ctx.beginPath();
						this.ctx.lineWidth = 1;
						this.ctx.strokeStyle = 'red';
						this.ctx.strokeRect(x1, y1, x2 - x1, y2 - y1);

						console.log(item);
						//draw label area within box

						this.ctx.fillStyle = 'red';
						let textWidth = this.ctx.measureText(itemclass).width;
						let textHeight = parseInt(font, 10);
						this.ctx.fillRect(x1, y1, textWidth + 10, textHeight + 10);
						this.ctx.fillStyle = 'white';
						this.ctx.fillText(itemclass, x1, y1);
					}
				});
			}
		},
	},
	async mounted() {
		//load up a new model
		this.model = new cvstfjs.ObjectDetectionModel();
		await this.model.loadModelAsync('/models/model.json');
		//parse labels
		this.labels = labels.split('\n').map((e) => {
			return e.trim();
		});
	},
};
</script>

<style>
.home {
	font-family: 'Avenir', Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}

h1,
h2 {
	font-weight: normal;
}
</style>
