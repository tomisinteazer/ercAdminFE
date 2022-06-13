<script>
  import Counter from "./lib/Counter.svelte";
  import "./lib/Tailwind.css";
  let increment;
</script>

<section class="text-gray-600 body-font">
  <div class=" mx-auto flex px-5 py-24 items-center justify-center flex-col">
    <div class="text-center lg:w-5/6 w-full">
      <div class="my-8">
        <Counter bind:increment id="0" />
      </div>
      <div class="flex justify-center">
        <button
          class="inline-flex text-white bg-green-600 border-0 py-2 px-6 focus:outline-none hover:bg-green-900 rounded text-lg"
          on:click={increment}>Button</button
        >
        <button
          class="ml-4 inline-flex text-green-900 bg-gray-100 border-0 py-2 px-6 focus:outline-none hover:bg-gray-200 rounded text-lg"
          on:click={increment}>Button</button
        >
      </div>
    </div>
  </div>
</section>
