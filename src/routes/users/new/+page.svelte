<script>
  import { PUBLIC_BACKEND_BASE_URL } from '$env/static/public';
  import { goto } from '$app/navigation';
  import { authenticateUser } from './../../../utils/auth.js';
  let formErrors = {};
  let clicked = false;

  function postSignUp() {
    goto('/');
  }

  async function createUser(evt) {
    evt.preventDefault()
    clicked = true;

    if (evt.target['password'].value != evt.target['password-confirmation'].value) {
      formErrors['password'] = { message: 'Password confirmation does not match' };
      clicked = false;
      console.log(clicked);
      return;
    }

    const userData = {
      name: evt.target['name'].value,
      email: evt.target['email'].value,
      password: evt.target['password'].value
    };

    const resp = await fetch(PUBLIC_BACKEND_BASE_URL + '/users', {
      method: 'POST',
      mode: 'cors',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(userData)
    });

    if (resp.status == 200) {
      const res = await authenticateUser(userData.email, userData.password);

      if (res.success) {
        postSignUp();
      }
      
    }
      else {
      clicked = false;
      const res = await resp.json();
      formErrors = res.data;  
    } 
  }
</script>
<div class="bg-gradient-to-r from-purple-500 via-fuchsia-500 to-pink-500 pb-[100px]">
  <h1 class="text-center text-xl pt-[100px]">Create an Account</h1>
<div class="text-center hover">
    <a class="link-hover italic text-xs" href="/login">Already have an account? Click here to login instead!.</a>
</div>
<div class="flex justify-center items-center mt-8">
    <form on:submit={createUser} class="w-1/3">
        <div class="form-control w-full">
            <label class="label" for="name">
                <span class="label-text ">Username</span>
            </label>
            <input type="text" name="name" placeholder="johndoe" class="input input-bordered w-full" required />
            {#if 'name' in formErrors}
            <label class="label" for="name">
                <span class="label-text-alt text-red-500">{formErrors['name'].message}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full">
            <label class="label" for="email">
                <span class="label-text ">Email</span>
            </label>
            <input type="email" name="email" placeholder="john@example.com" class="input input-bordered w-full" required />
            {#if 'email' in formErrors}
            <label class="label" for="email">
                <span class="label-text-alt text-red-500">{formErrors['email'].message}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full">
            <label class="label" for="password">
                <span class="label-text ">Password</span>
            </label>
            <input type="password" name="password" placeholder="" class="input input-bordered w-full" required />
            {#if 'password' in formErrors}
            <label class="label" for="password">
                <span class="label-text-alt text-red-500">{formErrors['password'].message}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full">
            <label class="label" for="password">
                <span class="label-text ">Confirm Password</span>
            </label>
            <input type="password" name="password-confirmation" placeholder="" class="input input-bordered w-full" required />
            {#if 'password' in formErrors}
            <label class="label" for="password">
                <span class="label-text-alt text-red-500">{formErrors['password'].message}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full mt-4">
          {#if clicked}
            <button class="btn btn-md btn-primary hover:btn-accent loading">Create an Account</button>
          {:else}
            <button class="btn btn-md btn-primary hover:btn-accent">Create an Account</button>
          {/if}
        </div>
    </form>
</div>
</div>