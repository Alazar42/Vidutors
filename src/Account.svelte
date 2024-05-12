<script>
    import Login from "./Login.svelte";
    import Register from "./Register.svelte";
    export let currentPage;

    let error = ""

	let users = [
		{
			"username":"milkeybear14",
			"password":"m1i2c3k4y5"
		}
	]

    const register = () => {
        console.log("Registerd")
    }

	const login = (e) => {
		console.log("Logged In")
		users.forEach(user => {
			if (e.detail['username'] == user.username && e.detail['password'] == user.password){
			console.log(true)
			error = ""
		}else{
			error = "Error: User Not Found."
		}
		});
		
	}
</script>

<div>
    {#if currentPage == "Login"}
    <Login error={error} on:handleLogin={login}/>
    {:else if currentPage == "Register"}
    <Register error={error} on:handleRegister = {register}/>
    {/if}
</div>

<style>

</style>