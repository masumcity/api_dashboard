<template>
  <header class="text-gray-600 body-font">
    <div
      class="
        container
        mx-auto
        flex flex-wrap
        p-5
        flex-col
        md:flex-row
        items-center
      "
    >
      <a
        class="
          flex
          title-font
          font-medium
          items-center
          text-gray-900
          mb-4
          md:mb-0
        "
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          stroke="currentColor"
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          class="w-10 h-10 text-white p-2 bg-indigo-500 rounded-full"
          viewBox="0 0 24 24"
        >
          <path
            d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"
          ></path>
        </svg>
        <span class="ml-3 text-xl">API Data</span>
      </a>
      <nav
        class="md:ml-auto flex flex-wrap items-center text-base justify-center"
      >
        <nuxt-link to="/" class="mr-5 hover:text-gray-900"> Home </nuxt-link>
        <nuxt-link to="/categories" class="mr-5 hover:text-gray-900">
          Categories
        </nuxt-link>
        <nuxt-link to="/brands" class="mr-5 hover:text-gray-900">
          Brands
        </nuxt-link>
        <nuxt-link to="/products" class="mr-5 hover:text-gray-900">
          Products
        </nuxt-link>
      </nav>
       <form
            @submit.prevent="search(name)"
          >
      <input type="text" id="search" name="search" placeholder="Search name" v-model="name" class="inline-flex bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out mr-2">
      <button
      @click="search(name)"
        class="
          inline-flex
          items-center
          bg-gray-600
          border-1
          py-1
          px-3
          focus:outline-none
          hover:bg-gray-200
          rounded
          text-white
          mt-4
          md:mt-0
        "
      >
        Search
       
      </button>
      </form>
    </div>
  </header>
</template>

<script>
export default{

  data(){
    return {
      name:null,
    }
  },

  methods:{
    search(){
      console.log(this.name);
      this.$router.push({ path: `/search/${this.name}` });
    }
  }
}
</script>