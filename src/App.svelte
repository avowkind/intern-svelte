<script>
	import Hero from './Hero.svelte';
	import EntryForm from './EntryForm.svelte'
	import Repo from './Repo.svelte'

	// const defaultCreds  = { email: 'ernest.rutherford@plantandfood.co.nz', secret: 'the secret of my success' }
	let creds = {} // = defaultCreds;
	let repo = {}
	const apiUrl = 'https://tweakplan.com/JavaScriptDemoSubmission-1.0/candidates'
	const getUrl = (creds) => `${apiUrl}?email=${creds.email}&secret=${creds.secret}`
	const patchUrl = (id) => `${apiUrl}/${id}`
	const fetcher = url => fetch(url).then(r => r.json())
	let editing = false
	const setEditing = (val) => editing = val

	const getRepoDetails = async () => {
		console.log(`getRepoDetails ${creds.email}`);
    setEditing(!editing)

    repo = await fetch(getUrl(creds), {
      method: 'GET',
      headers: { 'Content-Type': 'application/json' }
    }).then(r => r.json())

  }
</script>

<main>
	<Hero title='Andrew Watkins, Plant and Food Research Intern Coding Example' />
	<p>
		Enter your email and secret to retrieve your repository details or register a new one.
	</p>
	<EntryForm bind:creds={creds} on:submit={getRepoDetails} />
	<Repo repo={repo} />

</main>

<style>
	main {
		max-width: 240px;
		margin: 0 auto;
		/* background-color: #fafafa; */

	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>