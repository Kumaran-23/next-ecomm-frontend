<script>
    import { authenticateUser} from "../../utils/auth";
    import { goto } from '$app/navigation';
    import { alerts } from "../../utils/alert";
    
	let formErrors = {};
    let clicked = false;

    async function signIn(evt) {
        evt.preventDefault();
        clicked = true;

        const result = {
        email: evt.target['email'].value,
        password: evt.target['password'].value, 
        }


        const res = await authenticateUser(result.email, result.password)
        if (res.success) {
            alerts.clearAlert();
            goto('/')
        }
        else {
			alerts.setAlert('Incorrect email or Password', 'error');
            setTimeout(() => {
                alerts.clearAlert();
            }, 1000)
            clicked = false;
        }
    }
    
    
</script>

<div class="bg-gradient-to-r from-purple-500 via-fuchsia-500 to-pink-500 min-h-screen">
<h1 class="text-center text-2xl font-bold sm:text-3xl">Login</h1>
<div class="flex justify-center items-center mt-8 ">
    <form on:submit={signIn} class="w-1/3">
	<div class="form-control w-full">
		<label class="label" for="email">
			<span class="label-text text-xl ">Email</span>
		</label>
		<input type="text" name="email" placeholder="Type here" class="input input-bordered w-full" required />
		{#if 'username' in formErrors}
            <label class="label" for="email">
                <span class="label-text-alt text-red-500">{formErrors['username'].message}</span>
            </label>
        {/if}
	</div>
	<div class="form-control w-full">
		<label class="label" for="password">
			<span class="label-text text-xl ">Password</span>
		</label>
		<input type="password" name="password" placeholder="Type here" class="input input-bordered w-full" required />
		{#if 'password' in formErrors}
            <label class="label" for="password">
                <span class="label-text-alt text-red-500">{formErrors['password'].message}</span>
            </label>
        {/if}
	</div>
    <div class="form-control w-full mt-10">
            {#if clicked}
                <button class="btn loading btn-primary hover:btn-accent">Login</button>
            {:else}
                <button class="btn btn-primary hover:btn-accent">Login</button>
            {/if}
	</div>
	<div class="text-center">
    	<a class="link-hover italic text-xs" href="/users/new">Don't have an account yet? Click here to sign-up instead!.</a>
	</div>
</form>
</div>
</div>
