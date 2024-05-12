<script>
	import TopBar from './TopBar.svelte'
	import Account from './Account.svelte';
  import LatestTutorials from './LatestTutorials.svelte';

	let currentPage = "Home";

	const loginPage = () => {
		currentPage = 'Login'
	}

	const registerPage = () => {
		currentPage = 'Register'
	}

	const homePage = () => {
		currentPage = 'Home'
	}
</script>

<main>
	<TopBar on:Login = {loginPage} on:Register={registerPage} on:Home = {homePage}/>

	{#if currentPage != ""}
	<LatestTutorials currentPage={currentPage} />
	<Account currentPage={currentPage} />
	{/if}
	<br>
	
</main>

<style>

</style>