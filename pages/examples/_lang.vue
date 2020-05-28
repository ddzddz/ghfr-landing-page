<template>
  <div>
    <div v-if="fetchState">
      loading...
    </div>
    <div v-else>
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
            <a :href="content.buttonLink" target="_blank">
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
      <footer class="font-sans bg-black text-white py-8 px-4">
        <div class="mx-auto max-w-xl overflow-hidden flex justify-between items-center">
          <ul class="text-sm text-gray-700 list-none p-0 flex items-center">
            <li>
              <a href="/" class="block mr-4 w-32">
                <img src="https://stitches.hyperyolo.com/images/logo-white.png" class alt="logo">
              </a>
            </li>
            <li>
              <a
                href="#"
                class="inline-block py-2 px-3 text-gray-500 hover:text-gray-500-light no-underline"
              >Product</a>
            </li>
            <li>
              <a
                href="#"
                class="inline-block py-2 px-3 text-gray-500 hover:text-gray-500-light no-underline"
              >Company</a>
            </li>
            <li>
              <a
                href="#"
                class="inline-block py-2 px-3 text-gray-500 hover:text-gray-500-light no-underline"
              >FAQs</a>
            </li>
            <li>
              <a
                href="#"
                class="inline-block py-2 px-3 text-gray-500 hover:text-gray-500-light no-underline"
              >About Us</a>
            </li>
          </ul>
          <p
            class="inline-block py-2 px-3 text-gray-700 text-xs"
          >
            ©2019 Hyperyolo. All rights reserved.
          </p>
        </div>
      </footer>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      fetchState: false,
      content: {}
    }
  },
  computed: {
    lang () {
      return this.$route.params.lang || 'fr'
    }
  },
  async mounted () {
    await this.getContent()
  },
  methods: {
    async getContent () {
      this.fetchState = true
      const data = await this.$axios
        .$get(
          'https://v2-api.sheety.co/612035a23ef10236acde20367e8a78e8/ghfr/feuille1'
        )
        .then(data => data.feuille1)
        .catch(err => err)
      this.content = data.filter(el => el.lang === this.lang)[0]
      this.fetchState = false
    }
  }
}
</script>
