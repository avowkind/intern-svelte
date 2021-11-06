<script>
	import { createEventDispatcher } from 'svelte';

	export let creds = {
		email: '',
		secret: ''
	};

	const dispatch = createEventDispatcher();
	const submit = () => dispatch('submit');

</script>

<div>
	<label for='email'>Email:</label>
	<input name='email' placeholder='your email address' bind:value={creds.email}>
	<label for='secret'>Secret:</label>
	<input
		name='secret' 
		type='password' 
		placeholder='your secret'  
		bind:value={creds.secret}
	>
	<button on:click={submit}>submit</button>
</div>

<style>
	div {
		display: flex;
		flex-direction: column;
		max-width: 400px;
	}
	input {
		margin-bottom: 10px;
	}
</style>