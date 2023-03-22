<script>
	let todos = []

	let task = "";

		let filter='all';

		function addTask(){
			todos = [{
				task:task,
				status:"pending"
			}, ...todos];
			task = "";
		}

		function markComplete(i){
			todos[i].status = "completed";
			todos = [...todos];
		}

		function removeTask(i){
			todos.splice(i,1);
			todos = [...todos];
		}

	</script>
	
	


	
	<div class="container">
		<div class="todo">
			<div class="form">
				<input type="text" bind:value={task}/>
				<button on:click={addTask}>
					Crear
				</button>
			</div>
			<div class="tasks">
				{#each todos as todo, i}
					{#if filter=='all'}
						<div class="task">
							<div>
								{todo.task}
							</div>
							<button class="{todo.status=='completed'?'active':''}" on:click={()=>{markComplete(i)}}>
								&#10004;
							</button>
							<button on:click={()=>{removeTask(i)}}>
								&#10006;
							</button>
						</div>
					{:else if filter=='completed'}
						{#if todo.status=='completed'}
							<div class="task">
								<div>
									{todo.task}
								</div>
								<button on:click={()=>{removeTask(i)}}>
									&#10006;
								</button>
							</div>
						{/if}
					{:else}
						{#if todo.status=='pending'}
							<div class="task">
								<div>
									{todo.task}
								</div>
								<button class="{todo.status=='completed'?'active':''}" on:click={()=>{markComplete(i)}}>
									&#10004;
								</button>
							</div>
						{/if}
					{/if}
				{/each}
			</div>
			<div class="filters">
				<button class="{filter=='all'?'active':''}" on:click={()=>{filter='all'}}>
					Todo
				</button>
				<button class="{filter=='completed'?'active':''}" on:click={()=>{filter='completed'}}>
					Completadas
				</button>
				<button class="{filter=='incomplete'?'active':''}" on:click={()=>{filter='incomplete'}}>
					Incompletas
				</button>
			</div>
		</div>
	</div>


	<style>
		* {
			margin:0px;
			padding:0px
		}
		.container {
			width:100%;
			height:100vh;
			background:#040a094f;
			display:flex;
			justify-content:center;
			align-items:center;
		}
		.todo {
			padding:20px;
			background:#f5f5f5;
			width:250px;
			border-radius:20px;
		}
		.todo > div {
			margin:20px 0px;
		}
		.todo .form{
			display:flex;
		}
		.todo .form input,
		.todo .form button {
			border:1px solid #638a99;
			height:40px;
			outline:none;
			border-radius:20px;
		}
		.todo .form input {
			flex:1;
			text-indent:20px;
		}
		.todo .form button {
			width:60px;
			margin-left:5px;
			color:#638a99;
			cursor:pointer;
		}
		.todo .tasks {
			min-height:100px;
		}
		.todo .tasks > .task {
			margin:10px 0px;
			display:flex;
		}
		.todo .tasks > .task > div {
			flex:1;
		}
		.todo .tasks > .task > button {
			width:25px;
			height:25px;
			border:1px solid #638a99;
			color:#638a99;
			border-radius:50%;
			margin:0px 5px;
			cursor:pointer;
		}
		.todo .tasks > .task > button.active{
			background:#638a99;
			color:#f5f5f5;
		}
		.todo .filters {
			display:flex;
			justify-content:space-between;
		}
		.todo .filters > button {
			padding:10px 8px;
			border:1px solid #638a99;
			color:#638a99;
			border-radius:20px;
			cursor:pointer;
		}
		.todo .filters > button.active {
			background:#638a99;
			color:#f5f5f5;
		}
	</style>