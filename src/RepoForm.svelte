<script>
	import { createEventDispatcher } from 'svelte';

	export let url = '';
	const dispatch = createEventDispatcher();
	const submit = () => dispatch('submit');

</script>

<div class='form'>
	<label for='url'>Repo URL</label>
	<input name='url' placeholder='new Repository URL' bind:value={url}>
	<p>&nbsp;</p><button on:click={submit}>submit</button>
</div>
