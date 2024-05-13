<script>
  import { createEventDispatcher } from "svelte";

  let dispatch = createEventDispatcher();

  export let error;
  let username;
  let password;
  let rememberMe = false;

  const handleLogin = () => {
    if (username && password) {
      error = ""
      const user = {
        username,
        password,
      };
      dispatch("handleLogin", user);
      console.log(username, password, rememberMe);
    } else {
      error = "Fill The Required Fields."
    }
  };
</script>

<div style="width:80%; margin-left: 10%" class="">
  <div class="adwa-red adwa-center"><h1>Login</h1></div>
  <div>
    {#if error}
        <p class="adwa-codespan adwa-center adwa-pale-red">{error}</p>
    {/if}
    <br />
    <form on:submit|preventDefault={handleLogin}>
      <input
        bind:value={username}
        class="adwa-input"
        type="text"
        name="username"
        id="username"
        placeholder="Enter Username ..."
      />
      <br />
      <input
        bind:value={password}
        class="adwa-input"
        type="password"
        name="password"
        id="password"
        placeholder="Enter Password ..."
      />
      <br />
      <span class="adwa-right">
        <span>Remember Me</span>
        <input
          on:input={() => (rememberMe = !rememberMe)}
          class="adwa-check"
          type="checkbox"
          name="RememberMe"
          id="rememberMe"
        />
      </span>
      <br />
      <br />
      <div class="adwa-center adwa-bottombar adwa-border-red adwa-padding">
        <input
          class="adwa-hover-green adwa-button adwa-red adwa-round"
          type="submit"
          value="Login"
        />
    </div>
    </form>
  </div>
</div>

<style>
</style>
