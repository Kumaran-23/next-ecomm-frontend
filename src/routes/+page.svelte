<script>
	import humanize from 'humanize-plus';
	export let data;
</script>

<!-- <div class="flex items-center">
  <div class="overflow-hidden text-center flex flex-col items-center"> -->
<!-- <div class="mt-6 mb-5 card w-4/6 bg-primary hover:bg-accent-focus shadow-xl hover:transition delay-150 hover:translate-x-16 hover:skew-x-6 ">
      <div class="card-body">
        <a class="font-bold text-2xl" href="/image/{image.url}">{image.title}
          <img src={image.url} alt={image.discription}>
        </a>
        <div class="text-sm mt-1">
          <span class="text-sm">USD {humanize.formatNumber(image.price)}</span>
        </div>
        <div class="italic text-xs opacity-50 mt-2">posted {new Date(image.uploaded_at).toLocaleDateString(undefined, { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric'})}</div>
      </div>
      <div class="mt-2 card-body">
        {image.discription.slice(0, 240)}...
      </div>
    </div> -->

<!-- <div class="flex justify-center">
      <div class="flex flex-wrap justify-center gap-4">
      {#each data.images as image}
      <div class="card hover:transition delay-150 hover:-translate-y-16 shadow-xl w-full sm:w-1/2 md:w-1/3 lg:w-1/4 xl:w-1/4">
        <div class="card-body bg-fuchsia-500">
          <img src={image.url} alt="" class="w-full h-1/2 object-cover pt-4">
          <h3 class="text-xl font-medium text-gray-800">{image.title}</h3>
          <p class="text-gray-600">{image.discription}</p>
        </div>
      </div>
  {/each}
    </div>
    </div> -->
<!-- <div class="flex justify-center mt-4">
	<div class="flex flex-wrap justify-center gap-6">
		{#each data.images as image}
			<div
				class="card hover:transition delay-150 hover:-translate-y-16 shadow-xl shadow-violet-600 w-full sm:w-1/2 md:w-1/3 lg:w-1/4 xl:w-1/4"
			>
				<figure style="height: 400px;">
					<img src={image.url} alt="" class="w-full h-full object-cover" />
				</figure>
				<div class="card-body">
					<h2 class="card-title">{image.title}</h2>
					<p>{image.discription}</p>
					<p>${image.price} USD</p>
					<div class="card-actions justify-end">
            <a href="/images/{image.id}"><button class="btn btn-primary hover:animate-pulse">View</button></a>
					</div>
				</div>
			</div>
		{/each}
	</div>
</div> -->
<div class="bg-gradient-to-r from-purple-500 via-fuchsia-500 to-pink-500">
  <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-3 gap-10 mx-auto pt-20 pb-10" style="width: 1200px;">
  {#each data.images as image}
    <div class="card hover:transition delay-150 hover:-translate-y-10 shadow-xl shadow-accent hover:shadow-red-500 flex flex-col justify-between">
      <figure style="height: 300px;" class="relative">
        <img src={image.url} alt="" class="w-full h-full object-cover transition-transform duration-300 transform hover:scale-110" />
      </figure>
      <div class="card-body flex-grow bg-gradient-to-r from-teal-500 via-green-500 to-lime-500 rounded-b-2xl">
        <h2 class="card-title text-lg font-bold mb-2">{image.title}</h2>
        <p class="mb-4">{image.description}</p>
        <p class="">${image.price} USD</p>
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



