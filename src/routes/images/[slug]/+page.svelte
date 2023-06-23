<script>
    export let data;
    import SvelteMarkdown from 'svelte-markdown';
</script>

<!-- <div>
    <div class="flex">
        <img src={data.image.url} alt="" style="height:500px; width:500px;" class="pr-10 pl-10 rounded border border-black-300 p-4">
    </div>
        <div>
            <p>{data.image.title}</p>
            <p>{data.image.discription}</p>
            <p>{data.image.price}</p>
        </div>
</div> -->
<div class="container px-6 py-10 mx-auto flex justify-center items-center bg-gradient-to-r from-purple-500 via-fuchsia-500 to-pink-500">
    <div class="mt-8 lg:-mx-6 lg:flex lg:items-center">
        <img class="card w-1/2 mr-10 mb-10 shadow-xl shadow-accent hover:shadow-red-500" src={data.image.url} alt="">

        <div class="lg:w-2/3 lg:mt-0 lg:mx-6 ">
            <p class="text-xl font-extrabold text-blue-500 uppercase">{data.image.title}</p>
            <SvelteMarkdown class="mt-3" source={data.image.discription}/>

            <div class="flex items-center mt-6">
                <button class="btn btn-primary hover:btn-accent">Buy Now</button>
            </div>
        </div>
    </div>
</div>
