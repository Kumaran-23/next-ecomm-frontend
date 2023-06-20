<script>
    import "../app.css";
    import { isLogged, logOut } from "../utils/auth";
    import { goto } from '$app/navigation';

    function logIn() {
        goto('/login')
  }

    function signOut() {
        logOut();
        goto("/")
  }

  function goToImageUpload() {
    goto('/images/new')
  }
</script>
<div class="flex mb-10">
  <div class="mr-auto">
    <button class="btn btn-primary hover:btn-accent">
    <a href="/">Home</a>
  </button>
  </div>
  <div class="flex flex-wrap justify-end ">
  {#if $isLogged}
    <button class="btn mr-6 btn-primary hover:btn-accent" on:click={goToImageUpload}>Upload Image</button>
  <!-- {:else}
      <button class="btn mr-6 btn-primary hover:btn-accent" on:click={goToImageUpload}>Post a Job</button> -->
  {/if}
  {#if $isLogged}
      <button class="btn mr-6 btn-primary hover:btn-accent" on:click={signOut}>Log Out</button>
  {:else}
      <button class="btn mr-6 btn-primary hover:btn-accent" on:click={logIn}>Log In</button>
  {/if}
  {#if !$isLogged}
    <button class="btn mr-6 btn-primary hover:btn-accent">
      <a href='/users/new'>Create Account</a>
    </button>
  {/if}
  </div>
</div>