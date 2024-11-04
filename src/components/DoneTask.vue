<template>
	<li>
		<div class="base-card">
			<header>
				<h3>
					{{ title }}
					<button @click="deleteTask(id)"></button>
				</h3>
			</header>
		</div>
	</li>
</template>
<script>
export default {
	props: ["id", "title"],
	inject: ["deleteTask"],
};
</script>

<style scoped>
li {
	list-style: none;
	margin: auto;
}

button {
	padding: 10px 20px;
	height: 20px;
	width: 15px;
	border: none;
	border-radius: 5px;
	cursor: pointer;
	background-image: url("./asets/img/trash-filled.png");
	background-size: contain;
	background-color: transparent;
	background-position: center;
	background-repeat: no-repeat;
	transform: translateY(-50%);
}

button:hover {
	transform: translateY(-10px);
}
</style>
