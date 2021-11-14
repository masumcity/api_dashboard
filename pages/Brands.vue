<template>
  <div class="container mx-auto">
    <Nav />
    <section class="text-gray-600 body-font">
      <div class="container px-5 py-24 mx-auto">
        <div class="flex flex-col text-center w-full mb-10">
          <h1 class="sm:text-3xl text-2xl font-medium title-font text-gray-900">
            Total {{ total }} Brands
          </h1>
        </div>
        <div class="flex flex-wrap -m-2">
          <div
            v-for="brand in brands"
            :key="brand.id"
            class="p-2 lg:w-1/4 md:w-1/3 w-full"
          >
            <div
              class="
                h-full
                flex
                items-center
                border-gray-200 border
                p-4
                rounded-lg
              "
            >
              <div class="flex-grow">
                <h2 class="text-gray-900 title-font font-medium">
                  {{ brand.brands }}
                </h2>
                <p class="text-gray-500">Quantity - {{ brand.qty }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      brands: null,
      total: 0,
    };
  },

  mounted() {
    this.getBrands();
  },

  methods: {
    async getBrands() {
      await this.$axios
        .get("http://192.168.1.12:8077/Product/brand/1/2")
        .then((response) => {
          console.log(response.data);
          this.brands = response.data;
          this.total = response.data.length;
        });
    },
  },
};
</script>
