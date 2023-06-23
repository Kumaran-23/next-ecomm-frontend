<svelte:head>
  <script src="/aws-sdk-s3.min.js"></script>
</svelte:head>

<script>
  import { PUBLIC_BACKEND_BASE_URL } from '$env/static/public';
  import { goto } from '$app/navigation';
  import { getTokenFromLocalStorage } from '../../../utils/auth.js';
  import { uploadMedia } from '../../../utils/s3-uploader.js';
  let formErrors = {};
  let clicked = false; 

  function postJob() {
    goto('/');
  }

  async function uploadImage(evt) {
    evt.preventDefault();
    clicked = true;
    const [fileName, fileUrl] = await uploadMedia(evt.target['file'].files[0]);
    const token = getTokenFromLocalStorage();

    const imageData = {
      title: evt.target['title'].value,
      discription: evt.target['description'].value,
      price: parseFloat(evt.target['price'].value),
      url: fileUrl,
    };

    const resp = await fetch(PUBLIC_BACKEND_BASE_URL + '/image', {
      method: 'POST',
      mode: 'cors',
      headers: {
        'Content-Type': 'application/json',
         Authorization : `Bearer ${token}`
      },
      body: JSON.stringify(imageData)
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

<h1 class="text-2xl text-center font-bold">Upload Image For Sale</h1>
<div class="flex justify-center items-center">
    <form on:submit={uploadImage} class="w-1/3 mt-10">
        <div class="form-control w-full mt-2 mb-5">
            <input type="file" name="file" class="w-1/2"/>
            {#if 'file' in formErrors}
            <label class="label" for="file">
                <span class="label-text-alt text-red-500">{formErrors['file']}</span>
            </label>
            {/if}
        </div>
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

        <!-- <div class="form-control w-full mb-3">
            <label class="label" for="url">
                <span class="label-text">url</span>
            </label>
            <input type="url" name="url" placeholder="link to image" class="input input-bordered w-full" required />
            {#if 'location' in formErrors}
            <label class="label" for="url">
                <span class="label-text-alt text-red-500">{formErrors['url'].message}</span>
            </label>
            {/if}
        </div> -->

        <div class="form-control w-full mb-3">
            <label class="label" for="price">
                <span class="label-text">Price</span>
            </label>
            <input type="text" name="price" placeholder="1200.00" class="input input-bordered w-full" required />
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
