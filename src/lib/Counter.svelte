<script>
  import logo from "../assets/svelte.png";
  import { getStore } from "./hmr-stores";
  export let id;
  const count = getStore(id, 0);

  let contract = "";
  let name = "";
  let short = "";
  let image = "";
  $: addedTokens = [];
  async function addNewToken() {
    let r = await fetch("https://nest-tokens-api.herokuapp.com/erc-tokens", {
      method: "POST",
      body: JSON.stringify({ name, contract, short, image }),
      headers: { "Content-type": "application/json; charset=UTF-8" },
    });
    let res = await r.json();
    getTokens();
    console.log(res);
    contract = "";
    name = "";
    short = "";
    image = "";
  }

  async function getTokens() {
    let Tokens = await fetch(
      "https://nest-tokens-api.herokuapp.com/erc-tokens",
      {
        method: "GET",
        headers: { "Content-type": "application/json; charset=UTF-8" },
      }
    );

    let res = await Tokens.json();
    addedTokens = [...res.ephemerals];
    return res.ephemerals;
  }
  async function remToken(id) {
    let r = await fetch("https://nest-tokens-api.herokuapp.com/erc-tokens", {
      method: "DELETE",
      body: JSON.stringify({ id }),
      headers: { "Content-type": "application/json; charset=UTF-8" },
    });
    let res = await r.json();
    console.log(res);
    getTokens();
    alert(res + " has been removed");
  }
  export const increment = () => {
    $count += 1;
  };

  setTimeout(() => {
    getTokens();
  }, 2000);
</script>

<div>
  <section class="text-gray-600 body-font relative">
    <div class=" px-5 py-24 mx-auto flex sm:flex-nowrap flex-wrap">
      <div
        class="lg:w-2/3 md:w-1/2 bg-gray-100 rounded-lg overflow-hidden sm:mr-10 p-10 flex items-end justify-center relative"
      >
        <div class="lg:w-11/12 text-center">
          <img
            class="lg:w-2/6 md:w-3/6 w-5/6 mb-10 object-cover object-center rounded-full"
            alt={image}
            style="display: inline;"
            src={image || logo}
          />
          <div
            class="bg-white relative flex flex-wrap py-6 rounded-lg shadow-lg "
          >
            <div class="flex flex-col text-center w-full mb-12">
              <h1 class=" font-medium title-font mb-4 ">Contract</h1>
              <p
                class="lg:w-2/3 mx-auto leading-relaxed text-base text-green-600"
              >
                {contract}
              </p>
            </div>
            <div class="w-1/2 px-6 mt-4 lg:mt-0">
              <h2
                class="title-font font-semibold text-gray-900 tracking-widest text-xs"
              >
                Token Name
              </h2>
              <a class="text-green-600 leading-relaxed" href="/#">{name}</a>
            </div>
            <div class=" w-1/2  px-6 mt-4 lg:mt-0">
              <h2
                class="title-font font-semibold text-gray-900 tracking-widest text-xs "
              >
                $SHORT
              </h2>
              <p class="leading-relaxed text-green-600">{short}</p>
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
            >Token Image URL</label
          >
          <input
            type="text"
            id="image"
            bind:value={image}
            name="image"
            class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
          />
        </div>
        <div class="relative mb-4">
          <label for="name" class="leading-7 text-sm text-gray-600"
            >Token fullName</label
          >
          <input
            type="text"
            id="name"
            bind:value={name}
            name="name"
            class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
          />
        </div>
        <div class="relative mb-4">
          <label for="short" class="leading-7 text-sm text-gray-600"
            >Token Short Name</label
          >
          <input
            type="text"
            id="short"
            name="short"
            bind:value={short}
            class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
          />
        </div>
        <div class="relative mb-4">
          <label for="contract" class="leading-7 text-sm text-gray-600"
            >Token Contract</label
          >
          <input
            id="contract"
            bind:value={contract}
            name="contract"
            class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 h-32 text-base outline-none text-gray-700 py-1 px-3 resize-none leading-6 transition-colors duration-200 ease-in-out"
          />
        </div>
        <button
          on:click={addNewToken}
          class="text-white bg-green-700 border-0 py-2 px-6 focus:outline-none hover:bg-green-900 rounded text-lg"
          >Add Token +
        </button>
        <p class="text-xs text-gray-500 mt-3">
          Chicharrones blog helvetica normcore iceland tousled brook viral
          artisan.
        </p>
      </div>
    </div>
    <div class="text-center">
      <button
        class="px-8 py-4 w-52 text-green-500 bg-green-200 rounded-full "
        {id}
        on:click={getTokens}
      >
        Clicks: {$count}
      </button>
    </div>
  </section>

  <section class="text-gray-600 body-font">
    <div class="container px-5 py-24 mx-auto">
      {#if !addedTokens.length}
        <div>loading ...</div>
      {/if}
      {#if addedTokens}
        <div class="flex flex-wrap -m-4">
          {#each addedTokens as data (data._id)}
            <div class="lg:w-1/4 md:w-1/2  p-4 ">
              <div
                class="w-full border-2 border-gray-200 border-opacity-60 p-4"
              >
                <a class="block relative h-48 rounded " href="/#">
                  <img
                    alt={data.image}
                    class="w-48 h-48 bg-gray-100 object-cover object-center flex-shrink-0 rounded-full mr-4"
                    src={data.image}
                  />
                </a>
                <div class="mt-4">
                  <h3
                    class="text-gray-500 text-xs tracking-widest title-font mb-1"
                  >
                    {data.name}
                  </h3>
                  <p class="text-gray-500 text-xs p-1 mb-1">
                    {data.contract}
                  </p>
                  <h2 class="text-gray-900 title-font text-lg font-medium">
                    {data.short}
                  </h2>
                  <button
                    class="text-red-700 bg-red-100 p-2 text-xs mt-4 rounded inline-flex items-center md:mb-2 lg:mb-0"
                    on:click={() => {
                      remToken(data._id);
                    }}
                    >Delete
                    <svg
                      style="transform: rotate(90deg);"
                      class="w-4 h-4 ml-1"
                      viewBox="0 0 24 24"
                      stroke="currentColor"
                      stroke-width="2"
                      fill="none"
                      stroke-linecap="round"
                      stroke-linejoin="round"
                    >
                      <path d="M5 12h14" />
                      <path d="M12 5l7 7-7 7" />
                    </svg>
                  </button>
                  <button
                    class="text-green-700 bg-green-100 p-2 text-xs mt-4 rounded inline-flex items-center md:mb-2 lg:mb-0"
                    on:click={() => {
                      alert("update feature will be added soon");
                    }}
                    >update
                    <svg
                      style="transform: rotate(-90deg);"
                      class="w-4 h-4 ml-1"
                      viewBox="0 0 24 24"
                      stroke="currentColor"
                      stroke-width="2"
                      fill="none"
                      stroke-linecap="round"
                      stroke-linejoin="round"
                    >
                      <path d="M5 12h14" />
                      <path d="M12 5l7 7-7 7" />
                    </svg>
                  </button>
                </div>
              </div>
            </div>
          {/each}
        </div>
      {/if}
    </div>
  </section>
</div>
