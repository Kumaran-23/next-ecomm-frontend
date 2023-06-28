<script>
    export let data;
    import SvelteMarkdown from 'svelte-markdown';
    import { goto } from '$app/navigation';
    import { PUBLIC_BACKEND_BASE_URL } from '$env/static/public';
    import { getUserID, getTokenFromLocalStorage } from '../../../utils/auth.js';
    import { isLogged } from '../../../utils/auth.js';

    const userId =getUserID();

    async function checkout(id) {
      const resp = await fetch(PUBLIC_BACKEND_BASE_URL + '/checkout', {
      method: 'POST',
      mode: 'cors',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({id})

      });
      const res = await resp.json();
        goto(res)

    }

    async function deleteImage(id) {
    const token = getTokenFromLocalStorage();

    const resp = await fetch(PUBLIC_BACKEND_BASE_URL + `/image/${data.image.id}`, {
      method: 'DELETE',
      mode: 'cors',
      headers: {
        'Content-Type': 'application/json',
         Authorization : `Bearer ${token}`
      },
      body: JSON.stringify({id})
    });

    if (resp.status === 200) {
        goto('/');
      }
  }
</script>

<div class="container px-6 py-10 mx-auto flex justify-center items-center bg-gradient-to-r from-purple-500 via-fuchsia-500 to-pink-500">
    <div class="mx-6 flex items-center pt-10" style="width: 900px;">
        <div style="width:1000px;" class="mr-10">
                    <img class="card mr-10 mb-10 shadow-xl shadow-sky-200 hover:shadow-indigo-600" src={data.image.url} alt="" style="width:600px; height:600px;">        

            <div class="flex items-center justify-center mt-3">
            {#if $isLogged && (userId === data.image.userId)}
                <button class="btn btn-primary hover:btn-accent" type="button" on:click={deleteImage(data.image.id)}>Delete</button>
            {/if}
        </div>
        </div>
        <div class="lg:w-2/3 lg:mt-0 lg:mx-6 mb-40">
            <p class="text-3xl font-extrabold text-indigo-600 uppercase mb-5">{data.image.title}</p>
            <br>
            <p class="mt-3 mb-5 text-2xl text-indigo-600">{data.image.discription}</p>
            <br>
            <p class="mt-3 mb-5 text-2xl  text-indigo-600">USD {data.image.price/100}</p>
            <br>
            <div class="flex items-center mt-6">
                <button class="btn btn-primary hover:btn-accent" type="submit" on:click={checkout(data.image.id)}>Buy Now</button>
            </div>
        </div>
    </div>
</div>
