<script>
	import humanize from 'humanize-plus';
	export let data;


</script>

<div class="bg-gradient-to-r from-purple-500 via-fuchsia-500 to-pink-500">
  <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-3 gap-10 mx-auto pt-20 pb-10" style="width: 1200px;">
  {#each data.images as image}
    <div class="card hover:transition delay-150 hover:-translate-y-10 shadow-xl shadow-sky-400 hover:shadow-indigo-600 flex flex-col justify-between">
      <figure style="height: 300px;" class="relative">
        <img src={image.url} alt="" class="w-full h-full object-cover transition-transform duration-300 transform hover:scale-110" />
      </figure>
      <div class="card-body flex-grow bg-gradient-to-r from-green-500  to-teal-500 rounded-b-2xl">
        <h2 class="card-title text-lg font-bold mb-2">{image.title}</h2>
        <p class="mb-4">{image.discription}</p>
        <p class="">${image.price/100} USD</p>
        <div class="card-actions justify-end mt-4">
          <a href="/images/{image.id}">
            <button class="btn btn-primary hover:animate-pulse hover:btn-accent">View</button>
          </a>
        </div>
      </div>
    </div>
  {/each}
</div>
</div>



