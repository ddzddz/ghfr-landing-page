<template>
  <div>
    <nav
      class="font-sans bg-white text-center flex justify-between my-4 mx-auto container overflow-hidden"
    >
      <a href="/" class="block text-left">
        <img
          src="https://stitches.hyperyolo.com/images/logo.png"
          class="h-10 sm:h-10 rounded-full"
          alt="logo"
        >
      </a>
      <ul class="text-sm text-gray-700 list-none p-0 flex items-center">
        <li>
          <a
            href="#"
            class="inline-block py-2 px-3 text-gray-900 hover:text-gray-700 no-underline"
          >Products</a>
        </li>
        <li>
          <a
            href="#"
            class="inline-block py-2 px-3 text-gray-900 hover:text-gray-700 no-underline"
          >Pricing</a>
        </li>
        <li class="pr-2">
          <a
            href="#"
            class="inline-block py-2 px-3 text-gray-900 hover:text-gray-700 no-underline"
          >FAQs</a>
        </li>
        <li class="pl-2 border-l">
          <a
            href="#"
            class="inline-block py-2 px-3 text-gray-900 hover:text-gray-700 no-underline"
          >Log In</a>
        </li>
        <button class="bg-black hover:bg-text-gray-800 text-white ml-4 py-2 px-3">
          Sign Up
        </button>
      </ul>
    </nav>
    <section class="bg-gray-300 font-sans">
      <div class="container m-auto flex flex-col md:flex-row max-w-xl">
        <div class="flex flex-col w-full lg:w-1/2 justify-center items-start py-8">
          <label for="tagline" class="uppercase tracking-loose">{{ content.title }}</label>
          <h1 class="my-4 font-normal">
            {{ content.h1 }}
          </h1>
          <p class="leading-normal mb-4">
            {{ content.valueProposition }}
          </p>
          <a :href="content.buttonLink" target="_blank" rel="noopener">
            <button
              class="bg-transparent hover:bg-black text-black font-semibold hover:text-white py-2 px-4 border border-black hover:border-transparent"
            >
              {{ content.buttonText }}
            </button>
          </a>
        </div>
        <div class="w-full lg:w-1/2 lg:py-6">
          <img
            :src="content.img"
            alt="image"
            class="w-full"
          >
        </div>
      </div>
    </section>
    <section class="antialiased font-sans w-full bg-gray-300 text-left text-black py-8">
      <div class="container mx-auto max-w-xl py-8 font-normal leading-normal">
        <h3 class="text-2xl">
          Grow Your Business
        </h3>
        <p
          class
        >
          Build high performing teams, establish design practices, mentor and grow the next generation of great designers, and design interfaces and experiences.
        </p>
        <div class="max-w-sm mt-4 sm:flex">
          <input
            id="email"
            type="email"
            class="block w-full focus:outline-0 bg-white py-3 px-6 mb-2 sm:mb-0"
            name="email"
            placeholder="Enter your email"
            required
          >
          <button
            class="uppercase text-sm text-white focus:outline-0 w-full sm:w-auto bg-black hover:bg-gray-900 focus:bg-gray-300 tracking-wide px-6"
          >
            Subscribe
          </button>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  async asyncData ({ $axios, route }) {
    const id = route.params.id
    const data = await $axios
      .$get(
        'https://v2-api.sheety.co/612035a23ef10236acde20367e8a78e8/ghfr/feuille1'
      )
      .then(data => data.feuille1)
      .catch(err => err)
    const content = data.filter(el => el.id === id)[0]
    return { content }
  },
  head () {
    return {
      htmlAttrs: {
        lang: this.content.lang
      }
    }
  }

}
</script>
