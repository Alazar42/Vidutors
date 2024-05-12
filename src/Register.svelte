<script>
    import { createEventDispatcher } from "svelte";
  
    let dispatch = createEventDispatcher();
  
    export let error;
    let email;
    let fname;
    let lname;
    let username;
    let password;
    let rememberMe = false;
  
    const handleRegister = () => {
      if (username && password) {
        const user = {
          username,
          password,
        };
        dispatch("handleRegister", user);
        console.log(username, password, rememberMe);
      } else {
        console.log("Not Provided");
      }
    };
  </script>

<div style="width:50%; margin-left:25%" class="">
    <div class="adwa-red adwa-center"><h1>Register</h1></div>
    <div>
      {#if error}
          <p class="adwa-codespan adwa-center adwa-pale-red">{error}</p>
      {/if}
      <br />
      <form on:submit|preventDefault={handleRegister}>
        <input
          bind:value={fname}
          class="adwa-input"
          type="text"
          name="fname"
          id="fname"
          placeholder="Enter First Name ..."
        />
        <br />
        <input
          bind:value={lname}
          class="adwa-input"
          type="text"
          name="lname"
          id="lname"
          placeholder="Enter Last Name ..."
        />
        <br />
        <input
          bind:value={email}
          class="adwa-input"
          type="email"
          name="email"
          id="email"
          placeholder="Enter Email ..."
        />
        <br />
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
        
        <br />
        <br />
        <div class="adwa-center adwa-bottombar adwa-border-red adwa-padding">
          <input
            class="adwa-hover-green adwa-button adwa-red adwa-round"
            type="submit"
            value="Register"
          />
      </div>
      </form>
    </div>
  </div>