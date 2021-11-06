<script>
	import { createEventDispatcher } from 'svelte';

	export let creds = {
		email: '',
		secret: ''
	};

	const dispatch = createEventDispatcher();
	const submit = () => dispatch('submit');

</script>

<div class='form'>
	<label for='email'>Email</label>
	<input name='email' placeholder='your email address' bind:value={creds.email}>
	<label for='secret'>Secret</label>
	<input
		name='secret' 
		type='password' 
		placeholder='your secret'  
		bind:value={creds.secret}
	>
	<p>&nbsp;</p><button on:click={submit}>Submit</button>
</div>
