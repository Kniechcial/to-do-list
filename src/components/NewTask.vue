<template>
	<form @submit.prevent="submitData">
		<div>
			<p class="opis-naglowka">
				<label for="title">Nazwa</label>
			</p>
			<input
				v-model="defaultTitleText"
				placeholder="Wprowadź tytuł zadania..."
				id="title"
				name="title"
				type="text"
				ref="titleInput"
				@input="validate" />
			<p
				v-if="!correctInput"
				class="error-text">
				To pole jest wymagane!
			</p>
		</div>
		<div>
			<p class="opis-naglowka">
				<label for="description">Opis</label>
			</p>
			<textarea
				v-model="defaultDescriptionText"
				placeholder="Wprowadź opis zadania..."
				id="description"
				name="description"
				ref="descInput"></textarea>
		</div>
		<div>
			<label
				>Ważne zadanie
				<input
					class="checkBox"
					name="checkbox"
					type="checkbox"
					v-model="important" />
				Tak
			</label>
			<div>
				<button
					@click="checkInput"
					:disabled="!correctInput"
					type="submit">
					Dodaj zadanie
				</button>
			</div>
		</div>
	</form>
</template>
<script>
export default {
	inject: ["addTask"],
	data() {
		return {
			defaultTitleText: "",
			defaultDescriptionText: "",
			important: false,
			correctInput: true,
		};
	},
	watch() {},
	methods: {
		submitData() {
			const taskTitle = this.defaultTitleText;
			const taskDescritption = this.defaultDescriptionText;
			const importantValue = this.important;
			this.addTask(taskTitle, taskDescritption, importantValue);
			this.validateInput;
			this.defaultTitleText = "";
			this.defaultDescriptionText = "";
			this.important = false;
			this.correctInput = true;
		},
		checkInput() {
			if (this.defaultTitleText.trim() !== "") {
				this.correctInput = true;
			} else {
				this.correctInput = false;
			}
		},
		validate() {
			this.correctInput = true;
		},
	},
};
</script>
<style scoped>
div {
	display: grid;
	place-items: center;
}
button {
	background: limegreen;
	cursor: pointer;
	border-radius: 10px;
	box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
	gap: 8px;
}
button:hover {
	background-color: gold;
	box-shadow: 0 2px 8px black;
}
textarea {
	height: 70px;
	width: 200px;
}
input {
	width: 200px;
	margin-bottom: 5px;
}
.checkBox {
	cursor: pointer;
	margin-left: 40px;
	margin-right: 10px;
	margin-bottom: 30px;
	margin-top: 20px;
	width: 20px;
}
.error-text {
	color: red;
	font-size: 15px;
	margin-top: 1px;
}
.opis-naglowka {
	margin-top: 5 px;
	margin-bottom: 5px;
}
</style>
