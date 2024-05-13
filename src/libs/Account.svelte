<script>
  import Login from "./Login.svelte";
  import Register from "./Register.svelte";
  export let currentPage;

  let error = "";
  let isLogged = false;

  const register = async (e) => {
    await fetch("https://vidutorsbackendrestapi.onrender.com/api/v1/register/", {
      method: "POST",
      headers: { "Content-type": "application/json" },
      body: JSON.stringify({
        email: e.detail.email,
        username: e.detail.username,
        password: e.detail.password,
      }),
    });
    currentPage = "Login";
  };

  const login = async (e) => {
  try {
    const response = await fetch("https://vidutorsbackendrestapi.onrender.com/api/v1/login/", {
      method: "POST",
      headers: { "Content-type": "application/json" },
      body: JSON.stringify({
        username: e.detail.username,
        password: e.detail.password,
      }),
    });

    if (response.ok) {
      // If the response is successful, extract data and save it in cookies
      const data = await response.json();

      // Example: saving user token in a cookie named 'userToken'
      document.cookie = `VidutorsUser=${data.token}; path=/`;
      
	  currentPage = "Home"
	  window.location.reload()
    } else {
      // Handle error response
      error = "Error: Invaid Credintials"
    }
  } catch (error) {
    error = "Error occurred during login:";
  }
};

</script>

<div>
  {#if currentPage == "Login"}
    <Login {error} on:handleLogin={login} />
  {:else if currentPage == "Register"}
    <Register {error} on:handleRegister={register} />
  {/if}
</div>

<style>
</style>
