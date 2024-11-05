<template>
	<div class="background-naglowek">
		<h1 class="naglowek">Lista zadań</h1>
	</div>
	<div class="addTask-area">
		<NewTask></NewTask>
	</div>
	<ul>
		<p
			class="pusta-lista-zadan"
			v-if="storedResource.length === 0">
			Nie masz jeszcze żadnego zadania do zrobienia. Dodaj pierwsze zadanie.
			Powodzenia!
		</p>
		<LearningResource
			v-for="res in storedResource"
			:key="res.id"
			:task="res">
		</LearningResource>
	</ul>
	<div class="doneTask-area">
		<h3 class="task-completed">Zadania Zrobione:</h3>
		<p
			class="pusta-lista-zadan-zrobionych"
			v-if="doneTask.length === 0">
			Nie ukończyłeś jeszcze żadnego zadania. Powodzenia!
		</p>
		<ul>
			<DoneTask
				v-for="res in doneTask"
				:key="res.id"
				:id="res.id"
				:title="res.title"></DoneTask>
		</ul>
	</div>
</template>

<script>
import LearningResource from "./components/LearningResource.vue";
import NewTask from "./components/NewTask.vue";
import DoneTask from "./components/DoneTask.vue";
export default {
	components: { LearningResource, NewTask, DoneTask },
	data() {
		return {
			storedResource: [
				{
					id: "1",
					title: "First Task",
					description: "zadania do zrobienia",
					important: false,
				},
				{
					id: "2",
					title: "Second Task",
					description: "Więcej zadań do zrobienia",
					important: true,
				},
				{
					id: "3",
					title: "Third Task",
					description: " Jeszcze więcej zadań do zrobienia!",
					important: false,
				},
			],
			doneTask: [
				{
					id: "1",
					title: "Done Task 1",
					description: "zadanie wykonane",
					important: false,
				},
			],
		};
	},
	provide() {
		return {
			deleteTask: this.deleteTask,
			addTask: this.addTask,
			taskDone: this.taskDone,
		};
	},
	methods: {
		taskDone(taskID) {
			const taskToDone = this.storedResource.findIndex(
				(elementInStore) => elementInStore.id === taskID
			);
			this.doneTask.push(this.storedResource[taskToDone]);
			this.storedResource.splice(taskToDone, 1);
			this.addToLocalStorageDoneTask();
			this.addToLocalSorage();
			console.log(this.doneTask);
		},
		deleteTask(taskID) {
			const taskToDelete = this.doneTask.findIndex(
				(elementInStore) => elementInStore.id === taskID
			);
			this.doneTask.splice(taskToDelete, 1);
			this.addToLocalStorageDoneTask();
		},
		addTask(newTitle, newDescritption, newImportant) {
			const newTask = {
				id: newTitle,
				title: newTitle,
				description: newDescritption,
				important: newImportant,
			};
			this.storedResource.push(newTask);
			this.addToLocalSorage();
			console.log(this.storedResource);
		},
		addToLocalSorage() {
			localStorage.setItem(
				"storedResource",
				JSON.stringify(this.storedResource)
			);
		},
		addToLocalStorageDoneTask() {
			localStorage.setItem("doneTask", JSON.stringify(this.doneTask));
		},
	},
	created() {
		const storedWebData = localStorage.getItem("storedResource");
		if (storedWebData) {
			this.storedResource = JSON.parse(storedWebData);
		}
		const storedWebDoneData = localStorage.getItem("doneTask");
		if (storedWebDoneData) {
			this.doneTask = JSON.parse(storedWebDoneData);
		}
	},
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Comfortaa:wght@500&family=Nunito:wght@300;400&family=Open+Sans:wght@400;600&family=Raleway:wght@100;400;700&family=Titillium+Web:wght@200&display=swap");

* {
	box-sizing: border-box;
}

html {
	font-family: "Comfortaa", "Roboto", sans-serif;
}

body {
	margin: 0;
	background: linear-gradient(to right, #330867 0%, #30cfd0 100%);
}
.naglowek {
	margin: 0;
	background: linear-gradient(to right, #80ff72 0%, #7ee8fa 100%);
	background-color: #3a0061;
	width: 100%;
	padding: 1rem;
	justify-content: center;
	align-items: center;
	display: flex;
	background-clip: text;
	-webkit-text-fill-color: transparent;
}
.background-naglowek {
	background-color: #3a0061;
}
.doneTask-area {
	width: 300px;
	height: 500px;
	background: linear-gradient(
		to right,
		#80ff72 0%,
		#7ee8fa 100%
	); 
	position: fixed;
	top: 50%; 
	right: 0; 
	transform: translateY(-50%); 
	border-radius: 12px; 
	overflow: auto; 
}

.addTask-area {
	width: 270px;
	height: 300px;
	background: linear-gradient(
		to left,
		#80ff72 0%,
		#7ee8fa 100%
	); 
	position: fixed;
	top: 50%; 
	left: 0; 
	transform: translateY(-50%); 
	border-radius: 12px; 

}
.task-completed {
	display: grid;
	place-items: center;
}
.pusta-lista-zadan {
	border-radius: 12px;
	box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
	padding: 20px;
	margin: 40px auto;
	margin-top: 80px;
	max-width: 800px;
	background: linear-gradient(to right, #80ff72 0%, #7ee8fa 100%);
	text-align: center;
	text-transform: uppercase;
}
.pusta-lista-zadan-zrobionych {
	margin-top: 80px;
	margin-left: 15px;
}
</style>
