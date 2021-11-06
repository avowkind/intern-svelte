<script>
  	export let repo = {
      "id": 44624,
      "email": "ernest.rutherford@plantandfood.co.nz",
      "secret": "the secret of my success",
      "repoURL": "https://github.com/avowkind/intern-test",
      "created": "2021-10-30T23:13:55.124736Z",
      "modified": "2021-10-31T21:12:52.861074Z"
    };
var today  = new Date();
</script>


{#if repo.repoURL}
<div>
  <h2>{repo.email}</h2>
  <p>
    <a href={repo.repoURL} isExternal>{repo.repoURL}</a>
  </p>
  <p>Created: {Date(repo.created).toLocaleString()}</p>
  <p>Modified: {Date(repo.modified).toLocaleString()}</p>
</div>
{/if}

<style>
  div {
    /* border: 1px solid black; */
    border-radius: 5px;
    box-shadow: 0 0 4px rgb(114, 134, 124); 
    padding: 10px;
    margin: 10px;
  }
</style>