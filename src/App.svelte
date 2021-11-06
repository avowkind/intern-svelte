<script>
	import Hero from './Hero.svelte';
	import EntryForm from './EntryForm.svelte'
	import Repo from './Repo.svelte'
	import RepoForm from './RepoForm.svelte';

	// These are the two main state variables:
	// creds - the user's credentials email and secret
	// repo - the details of the repo including id, URL, name, description, and owner
	const defaultCreds  = { email: 'ernest.rutherford@plantandfood.co.nz', secret: 'the secret of my success' }
	let creds = defaultCreds;
	let repo = {}

	// API paths to Get, Patch and Post to the server
	const apiUrl = 'https://tweakplan.com/JavaScriptDemoSubmission-1.0/candidates'
	const getUrl = (creds) => `${apiUrl}?email=${creds.email}&secret=${creds.secret}`
	const patchUrl = (id) => `${apiUrl}/${id}`
	
	// local state for showing and hiding the repo entry form
	let editing = false
	const setEditing = () => editing = true
	const unsetEditing = () => editing = false

	// Gets the repo details from the server based on the entered credentials
	// called by the EntryForm component submit button.
	const getRepoDetails = async () => {
    repo = await fetch(getUrl(creds), {
      method: 'GET',
      headers: { 'Content-Type': 'application/json' }
    }).then(r => r.json())
  }

	// Patches the repo details to the server with the new repo URL
	// called by the RepoForm component submit button.
	const updateRepoURL = async () => {
    unsetEditing()
    const patchData = { repoURL: repo.repoURL, secret: creds.secret }

    const res = await fetch(patchUrl(repo.id), {
      method: 'PATCH',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(patchData)
    })
		getRepoDetails()
  }

</script>

<main>
	<Hero title='Andrew Watkins, Coding Example in Svelte' />
	<p>
		Enter your email and secret to retrieve your repository details or register a new one.
	</p>
	<EntryForm bind:creds={creds} on:submit={getRepoDetails} />
	<Repo repo={repo} />
	{#if repo.repoURL}
		<button
			on:click={setEditing}
		>
			Edit Repo Details
		</button>
	{/if}
	{#if editing}
		<RepoForm bind:url={repo.repoURL} on:submit={updateRepoURL} />
	{/if}

</main>

<style>
	main {
		max-width: 240px;
		margin: 0 auto;
		/* background-color: #fafafa; */

	}

	@media (min-width: 640px) {
		main {
			max-width: 1024px;
		}
	}
</style>