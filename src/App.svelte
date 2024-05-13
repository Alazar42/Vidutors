<script>
	import TopBar from './libs/TopBar.svelte';
	import Account from './libs/Account.svelte';
  import LatestTutorials from './libs/LatestTutorials.svelte'

	let currentPage = "Home";

	const loginPage = () => {
		currentPage = 'Login'
	}

	const registerPage = () => {
		currentPage = 'Register'
	}

	export const homePage = () => {
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