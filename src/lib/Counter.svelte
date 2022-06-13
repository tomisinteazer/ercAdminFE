<script>
  import logo from "../assets/svelte.png";
  import { getStore } from "./hmr-stores";
  export let id;
  const count = getStore(id, 0);
  export const increment = () => {
    $count += 1;
  };
</script>

<div>
  <section class="text-gray-600 body-font relative">
    <div class=" px-5 py-24 mx-auto flex sm:flex-nowrap flex-wrap">
      <div
        class="lg:w-2/3 md:w-1/2 bg-gray-300 rounded-lg overflow-hidden sm:mr-10 p-10 flex items-end justify-center relative"
      >
        <div class="lg:w-11/12">
          <img
            class="lg:w-2/6 md:w-3/6 w-5/6 mb-10 object-cover object-center rounded"
            alt="hero"
            style="display: inline;"
            src={logo}
          />
          <div class="bg-white relative flex flex-wrap py-6 rounded shadow-md ">
            <div class="flex flex-col text-center w-full mb-12">
              <h1 class=" font-medium title-font mb-4 ">Contract</h1>
              <p
                class="lg:w-2/3 mx-auto leading-relaxed text-base text-green-600"
              >
                xxxxxxxxxxxxxxxxxxxxxxxxxxxxx
              </p>
            </div>
            <div class="w-1/2 px-6 mt-4 lg:mt-0">
              <h2
                class="title-font font-semibold text-gray-900 tracking-widest text-xs"
              >
                Name
              </h2>
              <a class="text-green-600 leading-relaxed" href="/#">name</a>
            </div>
            <div class=" w-1/2  px-6 mt-4 lg:mt-0">
              <h2
                class="title-font font-semibold text-gray-900 tracking-widest text-xs "
              >
                $
              </h2>
              <p class="leading-relaxed text-green-600">xxxx</p>
            </div>
          </div>
        </div>
      </div>
      <div
        class="lg:w-1/3 md:w-1/2 bg-white flex flex-col md:ml-auto w-full md:py-8 mt-8 md:mt-0"
      >
        <h2 class="text-gray-900 text-lg mb-1 font-medium title-font">
          Add new Erc20 Token
        </h2>
        <p class="leading-relaxed mb-5 text-gray-600">
          ensure that all Fields are filled and the image displays before
          sending
        </p>
        <div class="relative mb-4">
          <label for="name" class="leading-7 text-sm text-gray-600"
            >Token fullName</label
          >
          <input
            type="text"
            id="name"
            name="name"
            class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
          />
        </div>
        <div class="relative mb-4">
          <label for="short" class="leading-7 text-sm text-gray-600"
            >Short Name</label
          >
          <input
            type="text"
            id="short"
            name="short"
            class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
          />
        </div>
        <div class="relative mb-4">
          <label for="contract" class="leading-7 text-sm text-gray-600"
            >Token Contract</label
          >
          <input
            id="contract"
            name="contract"
            class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 h-32 text-base outline-none text-gray-700 py-1 px-3 resize-none leading-6 transition-colors duration-200 ease-in-out"
          />
        </div>
        <button
          class="text-white bg-green-700 border-0 py-2 px-6 focus:outline-none hover:bg-green-900 rounded text-lg"
          >Add Token +
        </button>
        <p class="text-xs text-gray-500 mt-3">
          Chicharrones blog helvetica normcore iceland tousled brook viral
          artisan.
        </p>
      </div>
    </div>
    <button
      class="px-8 py-4 w-52 text-green-500 bg-green-200 rounded-full"
      {id}
      on:click={increment}
    >
      Clicks: {$count}
    </button>
  </section>
</div>
