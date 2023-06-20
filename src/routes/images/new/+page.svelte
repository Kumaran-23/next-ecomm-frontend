<script>
  import { PUBLIC_BACKEND_BASE_URL } from '$env/static/public';
  import { goto } from '$app/navigation';
  import { getTokenFromLocalStorage } from '../../../utils/auth.js';
  let formErrors = {};
  let clicked = false; 

  function postJob() {
    goto("/");
  }

  async function uploadImage(evt) {
    evt.preventDefault();
    clicked = true;
    const getLocalData = getTokenFromLocalStorage();

    const imageData = {
      accessToken: getLocalData,
      title: evt.target['title'].value,
      description: evt.target['description'].value,
      prince: evt.target['price'].value,
      url: evt.target['url'].value
    };

    const resp = await fetch(PUBLIC_BACKEND_BASE_URL + '/image', {
      method: 'POST',
      mode: 'cors',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(jobData)
    });

    if (resp.status === 200) {
        postJob();
      }
      else {
      const res = await resp.json();
      formErrors = res.data;
      clicked = false;
    }
  }
</script>

<h1 class="text-xl text-center">Upload Image For Sale</h1>
<div class="flex justify-center items-center h-screen">
    <form on:submit={uploadImage} class="w-full max-w-xl">
        <div class="form-control w-full mb-3">
            <label class="label" for="title">
                <span class="label-text">Title</span>
            </label>
            <input type="text" name="title" placeholder="Misty Mountain Top" class="input input-bordered w-full" required />
            {#if 'title' in formErrors}
            <label class="label" for="title">
                <span class="label-text-alt text-red-500">{formErrors['title'].message}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full mb-3">
            <label class="label" for="description">
                <span class="label-text">Description</span>
            </label>
            <textarea name="description" placeholder="Beatiful view from atop of Mount Everest" class="textarea textarea-bordered h-20" ></textarea>
            {#if 'description' in formErrors}
            <label class="label" for="description">
                <span class="label-text-alt text-red-500">{formErrors['description'].message}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full mb-3">
            <label class="label" for="url">
                <span class="label-text">url</span>
            </label>
            <input type="url" name="url" placeholder="link to image" class="input input-bordered w-full" required />
            {#if 'location' in formErrors}
            <label class="label" for="url">
                <span class="label-text-alt text-red-500">{formErrors['url'].message}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full mb-3">
            <label class="label" for="price">
                <span class="label-text">Price</span>
            </label>
            <input type="number" name="price" placeholder="1200.00" class="input input-bordered w-full" required />
            {#if 'location' in formErrors}
            <label class="label" for="location">
                <span class="label-text-alt text-red-500">{formErrors['location'].message}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full mb-10">
            {#if clicked}
                <button class="btn btn-md btn-primary hover:btn-accent loading">Upload Image</button>
            {:else}
                <button class="btn btn-md btn-primary hover:btn-accent">Upload Image</button>
            {/if}
        </div>
    </form>
</div>
