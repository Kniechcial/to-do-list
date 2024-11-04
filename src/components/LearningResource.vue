<template>
	<li>
		<div
			:class="{
				'important-background-base-card': task.important,
				'background-base-card': !task.important,
			}">
			<div
				:class="{
					'important-base-card': task.important,
					'base-card': !task.important,
				}">
				<header>
					<h3>{{ task.title }}</h3>
					<button @click="taskDone(task.id)">Zadanie zrobione</button>
				</header>
				<p>{{ task.description }}</p>
			</div>
		</div>
	</li>
</template>
<script>
export default {
	props: ["task"],
	inject: ["taskDone"],
};
</script>

<style scoped>
li {
	list-style: none;
	margin: auto;
	max-width: 40rem;
}

header {
	display: flex;
	justify-content: space-between;
	align-items: center;
}

h3 {
	font-size: 1.25rem;
	margin: 0.5rem 0;
}

p {
	margin: 0.5rem 0;
}

.base-card {
	border-radius: 12px;
	box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
	padding: 20px;
	margin: 40px auto;
	max-width: 800px;
	background: linear-gradient(to right, #80ff72 0%, #7ee8fa 100%);
	background-clip: text;
	-webkit-text-fill-color: transparent;
}
.background-base-card {
	background: linear-gradient(to right, #30cfd0 0%, #330867 100%);
	border-radius: 12px;
}
.important-background-base-card {
	background: linear-gradient(to right, #f50404 0%, #ec2a03 100%);
	border-radius: 12px;
}
.important-base-card {
	border-radius: 12px;
	box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
	padding: 20px;
	margin: 40px auto;
	max-width: 800px;
	text-transform: uppercase;
}
button {
	background: #80ff72;
	background-clip: text;
	-webkit-text-fill-color: transparent;
	cursor: pointer;
	border-radius: 10px;
	box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
}
button:hover {
	background-color: gold;
	box-shadow: 0 2px 8px gold;
}
</style>
