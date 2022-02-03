

<script>
	let fav
	let val;
	// let elements={inp:"Text",correct:"XYZ"};

		
	// $: elements.inp=fav;
	// $: elements.correct=val;
	// $: console.log(elements);


	let list = [];
	let elements = {};
	let lastId = 0;
	let currentAdd = '';
	
	const handleAdd = (data) => {
		if (currentAdd === '') return;
		list = [...list, {
			id: lastId++,
			value: currentAdd
		}];
		currentAdd = '';
	};
	
	const handleRemove = (id) => {
		list = list.filter(item => item.id !== id);
	};
	
	// remove null values
	$: {
		let dirty = false;
		Object.getOwnPropertyNames(elements).forEach(key => {
			if (elements[key] === null) {
				delete elements[key];
				dirty = true;
			}
		});
		if (dirty) {
			// force reactivity
			elements = elements;
		}
	}
	// log changes to elements
	$: console.log(list);
	
	// $: {
	// 	let dirty = false;
	// 	Object.getOwnPropertyNames(elements).forEach(key => {
	// 		if (elements[key] === null) {
	// 			delete elements[key];
	// 			dirty = true;
	// 		}
	// 	});
	// 	if (dirty) {
	// 		// force reactivity
	// 		elements = elements;
	// 	}
	// }
	// // log changes to elements
	// $: console.log(elements);
</script>

<div class="container d-flex flex-column justify-content-start border border-dark w-50 mw-50 mh-50vw h-50vw px-0 py-0">
	<form on:submit|preventDefault={handleAdd}>
	<div class="bg-white clearfix border border-dark border-top-0 border-start-0 border-end-0">
		<select bind:value={fav}  class="mx-3 my-2 form-select form-select-sm w-50 d-inline-flex" aria-label="selectValues">
			<option selected>Text</option>
			<option value="Drop Down">Drop Down</option>
			<option value="Drag and Drop">Drag and Drop</option>
			<option value="Multiple Line">Multiple Line</option>
			<option value="Math Equation">Math Equation</option>
		</select>
		<button type="button" class="btn px-2 mx-2 py-1 my-1 bg-white float-end my-0">x</button>
	</div>
	{#if fav=="Text"}
	
		<p class="mx-3 my-2">Input type</p>
		<select class="mx-3 my-0 form-select form-select-sm w-50 d-inline-flex" aria-label="subSelect">
			<option selected>Text</option>
			<option value="Code">Code</option>
			<option value="Number">Number</option>
			<option value="Date">Date</option>
			<option value="Email">Email</option>
			<option value="Password">Password</option>
		</select>
		
		<div class="mb-3 mx-3 my-2">
			<label for="correct_answer" class="form-label">Correct Answer</label>
			<input type="text" class="form-control w-100 p-0" bind:value={currentAdd}  id="correct_answer" aria-describedby="correctAnswer">
		</div>
	
		<div class="form-check mx-3">
			<input class="form-check-input" type="checkbox" value="" id="first" checked>
			<label class="form-check-label" for="first">User can select any of the answers seperated by comma</label>
		</div>
		<div class="mb-2 mx-3">
			<label for="css_first" class="form-label">Style: (Write CSS)</label>
			<input type="text" class="form-control w-100 p-0" id="css_first" aria-describedby="writeCSS">
		</div>
	{:else if fav=="Drop Down"}
		<div class="mb-2 mx-3 pr-3 my-2">
			<label for="correct_second" class="form-label">Correct Answer</label>
			<div class="d-flex flex-row">
				<input class="form-check-input mt-2" type="radio" name="input_first" bind:value={currentAdd}  id="correct_second">
				<form role="button" class="input-group d-flex border border-rad r mx-2 flex-nowrap w-100 rounded" id="selection">
					<input type="text" class="form-control p-0 border-0 w-50 rounded" id="input_second" aria-describedby="correctAnswer">
					<span role="button" tabindex="-1" class="input-group-text bg-light border-0 bg-white pr-1 rounded " aria-label="badge" name="defaultButton" id="badge_first">
						<small>
							<span class="badge bg-secondary">Default</span>
						</small>
					</span>
				</form>
				<span class="mt-sm-1 ml-sm-2">
					<i class='fas fa-trash-alt'></i>
				</span>
			</div>
			<button class="btn btn-outline-primary my-3 mx-1">&#43; Add Option</button>
			<div class="mb-2 mx-1">
				<label for="css_second" class="form-label">Style: (Write CSS)</label>
				<form role="textbox" class="input-group d-flex border border-rad r mx-0 flex-nowrap w-100 rounded" id="form_second">
					<input type="text" class="form-control p-1 border-0 w-50 rounded" id="css_second" aria-describedby="writeCSS">
				</form>
				<p class="">Note: Select radio button to indicate correct answer</p>
			</div>
			
		</div>
		{:else if fav=="Drag and Drop"}
		<div class="mb-2 mx-3 pr-3 ">
			<!-- <label for="correct_second" class="form-label">Correct Answer</label> -->
			<div class="d-flex flex-row mt-3">
				<input class="form-check-input" type="checkbox" value="" id="flexCheckDisabled">
				<form role="textbox" class="input-group d-flex border border-rad r mx-2 flex-nowrap w-100 rounded" id="form_other">
					<input type="text" class="form-control p-0 border-0 w-50 rounded" id="input_second" aria-describedby="DragandDrop">
					<!-- <span role="button" tabindex="-1" class="input-group-text bg-light border-0 bg-white pr-1 rounded " aria-label="badge" name="defaultButton" id="badge_first">
						<small>
							<span class="badge bg-secondary">Default</span>
						</small>
					</span> -->
				</form>
				<span class="mt-sm-0 ml-sm-2">
					<i class='fas fa-trash-alt'></i>
				</span>
			</div>
			<button class="btn btn-outline-primary my-3 mx-1">&#43; Add Option</button>
			<div class="form-check mx-1">
				<input class="form-check-input" type="checkbox" value="" id="first">
				<label class="form-check-label" for="first">Disable drop option after single drop</label>
			</div>
			<div class="mb-2 mx-1 my-2">
				<label for="css_second" class="form-label">Style: (Write CSS)</label>
				<form role="textbox" class="input-group d-flex border border-rad r mx-0 flex-nowrap w-100 rounded" id="form_second">
					<input type="text" class="form-control p-1 border-0 w-50 rounded" id="css_second" aria-describedby="writeCSS">
				</form>
				<p class="">Note: Select checkbox for correct drop value</p>
			</div>
			
		</div>
		{:else if fav=="Math Equation"}
		<div class="mb-2 mx-3 pr-3 ">
			<!-- <label for="correct_second" class="form-label">Correct Answer</label> -->
			<div class="d-flex flex-row mt-3">
				<input class="form-check-input" type="checkbox" value="" id="flexCheckDisabled">
				<form role="textbox" class="input-group d-flex border border-rad r mx-2 flex-nowrap w-100 rounded" id="form_other">
					<input type="text" class="form-control p-0 border-0 w-50 rounded" id="input_second" aria-describedby="DragandDrop">
					<!-- <span role="button" tabindex="-1" class="input-group-text bg-light border-0 bg-white pr-1 rounded " aria-label="badge" name="defaultButton" id="badge_first">
						<small>
							<span class="badge bg-secondary">Default</span>
						</small>
					</span> -->
				</form>
				<span class="mt-sm-0 ml-sm-2">
					<i class='fas fa-trash-alt'></i>
				</span>
			</div>
			<button class="btn btn-outline-primary my-2 mx-1">&#43; Add Option</button>
			<div class="mb-2 mx-1">
				<label for="css_second" class="form-label">Style: (Write CSS)</label>
				<form role="textbox" class="input-group d-flex border border-rad r mx-0 flex-nowrap w-100 rounded" id="form_second">
					<input type="text" class="form-control p-1 border-0 w-50 rounded" id="css_second" aria-describedby="writeCSS">
				</form>
				<p class="d-inline-flex">Note: Click on the pencil icon to add/edit latext math equation Put cursor before and click add response button to make part of the equation required user input</p>
				
			</div>
			
		</div>
		{/if}
	<footer class="bg-white clearfix border border-dark border-0 my-1 mb-2 pb-2 pr-2">
		<button class="btn btn-primary mx-3 float-end">Ok</button>
		<button class="btn btn-outline-secondary bg-white float-end mx-1 text-dark">Cancel</button>
	</footer>
</form>
</div>

<form>
	<div class="form-group">
		<label for="text_first">Example textarea</label>
		<textarea class="form-control w-50" id="text_first" rows="3" col="2" contenteditable="true" bind:innerHTML="{list.length}" ></textarea>
	  </div>
</form>




<!-- <form on:submit|preventDefault={handleAdd}>
	<input type="text" bind:value={currentAdd}>
	<input type="text" bind:value={currentAdd}>
	<button>
		Add
	</button>
</form>

<p>
	{list.length} items in the list.
</p>
<p>
	{Object.keys(elements).length} bound elements.
</p>-->

<p>
	{#each list as {id,value} (id)}
	{value}
	{/each}
</p> 
