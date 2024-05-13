<script>
  import { onMount } from "svelte";
  import { beforeUpdate } from "svelte";
  import { createEventDispatcher } from "svelte";
  import Register from "./Register.svelte";

  let dispatch = createEventDispatcher();
    let isTabShowing = true
    const showTab = (e) => {
        isTabShowing = !isTabShowing
    }
    $: isLogged = false

    onMount(() => {
        checkLoginStatus();
    });

    beforeUpdate(() => {
        checkLoginStatus();
    });

    const checkLoginStatus = () => {
        if (document.cookie.includes("VidutorsUser")) {
            isLogged = true;
        } else {
            isLogged = false;
        }
    };

    const homeHandler = () => {
        dispatch('Home');
    }

    const registerHandler = () => {
        dispatch('Register')
    }

    const loginHandler = () => {
        dispatch('Login')
    }

    const logoutHandler = async () => {
    let authToken = document.cookie.split("VidutorsUser=")[1]; // Extract the token from the cookie
    if (authToken) {
        authToken = "Token " + authToken; // Prepend "Token " to the token

        try {
            await fetch("https://vidutorsbackendrestapi.onrender.com/api/v1/logout/", {
                method: "POST", // Assuming logout requires a POST request
                headers: {
                    "Authorization": authToken
                }
            });

            // If the logout request is successful, clear the token cookie
            document.cookie = "VidutorsUser=; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/;";

            // Update the isLogged state
            
            isLogged = false;
        } catch (error) {
            console.error("Error occurred during logout:", error);
        }
    }
};


</script>

<header>
    <!-- navbar for large screens -->
    <nav class="adwa-bar adwa-hide-small">
        <h1 class="adwa-button adwa-round adwa-red  adwa-hover-green">Vidutors</h1>
        <ul class="adwa-right adwa-margin-right nav">
            <!-- svelte-ignore a11y-click-events-have-key-events -->
            <ol on:click={homeHandler} class="adwa-button adwa-round adwa-red adwa-margin-right adwa-margin-top adwa-hover-green">HOME</ol>
            <ol class="adwa-button adwa-round adwa-red adwa-margin-right adwa-margin-top adwa-hover-green">TUTORIALS</ol>
            {#if isLogged}
            <!-- svelte-ignore a11y-click-events-have-key-events -->
            <ol on:click={logoutHandler} class="adwa-button adwa-round adwa-red adwa-margin-top adwa-hover-green">LOGOUT</ol>
            {:else}
            <!-- svelte-ignore a11y-click-events-have-key-events -->
            <ol on:click={registerHandler} class="adwa-button adwa-round adwa-red adwa-margin-right adwa-margin-top adwa-hover-green">REGISTER</ol>
            <!-- svelte-ignore a11y-click-events-have-key-events -->
            <ol on:click={loginHandler} class="adwa-button adwa-round adwa-red adwa-margin-top adwa-hover-green">LOGIN</ol>
            {/if}
        </ul>
    </nav>
    <!-- nav bar for small screens -->
    <nav class="adwa-bar adwa-hide-large adwa-hide-medium">
        <h1 class="adwa-button adwa-round adwa-red  adwa-hover-green">Vidutors</h1>
        <span><button class="adwa-button adwa-right  adwa-hover-white" on:click={() => showTab()}>
        {#if !isTabShowing}
        <i class="fa fa-times adwa-large adwa-margin adwa-text-red"></i>
        {:else}
        <i class="fa fa-bars adwa-large adwa-margin adwa-red"></i>
        {/if}
        </button></span>
        <ul class="adwa-dropdown" class:adwa-hide = {isTabShowing}>
            <!-- svelte-ignore a11y-click-events-have-key-events -->
            <ol on:click={homeHandler} style="width: 100%;" class="adwa-button adwa-round adwa-red adwa-bar adwa-hover-green">HOME</ol>
            <ol style="width: 100%;" class="adwa-button adwa-round adwa-red adwa-bar adwa-hover-green">TUTORIALS</ol>
            {#if isLogged}
            <!-- svelte-ignore a11y-click-events-have-key-events -->
            <ol on:click={logoutHandler} style="width: 100%;" class="adwa-button adwa-round adwa-red adwa-bar adwa-hover-green">LOGOUT</ol>
            {:else}
            <!-- svelte-ignore a11y-click-events-have-key-events -->
            <ol on:click={registerHandler} style="width: 100%;" class="adwa-button adwa-round adwa-red adwa-bar adwa-hover-green">REGISTER</ol>
            <!-- svelte-ignore a11y-click-events-have-key-events -->
            <ol on:click={loginHandler} style="width: 100%;" class="adwa-button adwa-round adwa-red adwa-bar adwa-hover-green">LOGIN</ol>
            {/if}
        </ul>
    </nav>
</header>

<style>
    .nav{
        display: flex;
        list-style: none;
    }
</style>