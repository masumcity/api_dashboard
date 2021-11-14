<template>
  <div class="container mx-auto">
    <Nav />
    <section v-if="products" class="text-gray-600 body-font">
      <div class="container px-5 py-24 mx-auto">
        <div class="flex flex-col text-center w-full mb-10">
          <h1 class="sm:text-3xl text-2xl font-medium title-font text-gray-900">
            Total {{ total }} Products
          </h1>
        </div>

            <button
          type="button"
          @click="first"
          class="
            text-white
            bg-indigo-500
            border-0
            py-2
            px-8
            focus:outline-none
            hover:bg-indigo-600
            rounded
            text-lg
          "
        >
          First Page
        </button>
        <button
          type="button"
          v-if="prev_page_url"
          @click="prev"
          class="
            text-white
            bg-indigo-500
            border-0
            py-2
            px-8
            focus:outline-none
            hover:bg-indigo-600
            rounded
            text-lg
          "
        >
          {{ prev_page }}
        </button>
        <button
          type="button"
          v-else
          class="
            text-white
            bg-indigo-300
            border-0
            py-2
            px-8
            focus:outline-none
            rounded
            text-lg
          "
          disabled
        >
          No Previous Page
        </button>
        <button
          type="button"
          v-if="next_page_url"
          @click="next"
          class="
            text-white
            bg-indigo-500
            border-0
            py-2
            px-8
            focus:outline-none
            hover:bg-indigo-600
            rounded
            text-lg
          "
        >
          {{ next_page }}
        </button>
        <button
          type="button"
          v-else
          class="
            text-white
            bg-indigo-300
            border-0
            py-2
            px-8
            focus:outline-none
            rounded
            text-lg
          "
          disabled
        >
          No Next Page
        </button>
         <button
          type="button"
          @click="last"
          class="
            text-white
            bg-indigo-500
            border-0
            py-2
            px-8
            focus:outline-none
            hover:bg-indigo-600
            rounded
            text-lg
          "
        >
          Last Page
        </button>

        <div class="flex flex-wrap -m-2">
          <div
            v-for="product in products"
            :key="product.id"
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
                <h2 class="text-blue-700 title-font font-medium">
                  {{ product.name }}
                </h2>
                <p class="text-gray-500">Brand - {{ product.brand_name }}</p>
                <p class="text-gray-500">Short Des - {{ product.short_des }}</p>
                <p class="text-gray-500">
                  Vendor Price - {{ product.vendorprice }}
                </p>
                <p class="text-gray-500">
                  Retail Price - {{ product.retailprice }}
                </p>
                <p class="text-gray-500 text-red-600">
                  Quantity - {{ product.qty }}
                </p>
                <p class="text-gray-500">
                  Category Name - {{ product.category.name }}
                </p>
                <p class="text-gray-500">
                  Sub Category Name - {{ product.subCategory.name }}
                </p>
              </div>
            </div>
          </div>
        </div>
        <button
          type="button"
          @click="first"
          class="
            text-white
            bg-indigo-500
            border-0
            py-2
            px-8
            focus:outline-none
            hover:bg-indigo-600
            rounded
            text-lg
          "
        >
          First Page
        </button>
        <button
          type="button"
          v-if="prev_page_url"
          @click="prev"
          class="
            text-white
            bg-indigo-500
            border-0
            py-2
            px-8
            focus:outline-none
            hover:bg-indigo-600
            rounded
            text-lg
          "
        >
          {{ prev_page }}
        </button>
        <button
          type="button"
          v-else
          class="
            text-white
            bg-indigo-300
            border-0
            py-2
            px-8
            focus:outline-none
            rounded
            text-lg
          "
          disabled
        >
          No Previous Page
        </button>
        <button
          type="button"
          v-if="next_page_url"
          @click="next"
          class="
            text-white
            bg-indigo-500
            border-0
            py-2
            px-8
            focus:outline-none
            hover:bg-indigo-600
            rounded
            text-lg
          "
        >
          {{ next_page }}
        </button>
        <button
          type="button"
          v-else
          class="
            text-white
            bg-indigo-300
            border-0
            py-2
            px-8
            focus:outline-none
            rounded
            text-lg
          "
          disabled
        >
          No Next Page
        </button>
         <button
          type="button"
          @click="last"
          class="
            text-white
            bg-indigo-500
            border-0
            py-2
            px-8
            focus:outline-none
            hover:bg-indigo-600
            rounded
            text-lg
          "
        >
          Last Page
        </button>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      prev_page: "Previous Page",
      next_page: "Next Page",
      products: null,
      perpage: 20,
      total: 0,
      page_no: 1,
      prev_page_url: null,
      next_page_url: null,
      first_page: null,
      last_page: null,
    };
  },

  mounted() {
    this.getProducts();
  },

  methods: {
    async getProducts() {
      await this.$axios
        .get(
          `http://192.168.1.12:8077/Product/allproduct/1/${this.perpage}?page_no=${this.page_no}`
        )
        .then((response) => {
          // console.log(response.data.next_page_url);
          this.products = response.data.data;
          this.total = response.data.total;
          this.next_page_url = response.data.next_page_url;
          this.prev_page_url = response.data.prev_page_url;
          this.first_page = response.data.first_page_url;
          this.last_page = response.data.last_page_url;
        });
    },

    async next() {
      this.next_page = "Loading...";
      await this.$axios
        .get(`http://192.168.1.12:8077${this.next_page_url}`)
        .then((response) => {
          this.products = response.data.data;
          this.total = response.data.total;
          this.next_page_url = response.data.next_page_url;
          this.prev_page_url = response.data.prev_page_url;
          this.next_page = "Next Page";
        });
    },

    async prev() {
      this.prev_page = "Loading...";
      await this.$axios
        .get(`http://192.168.1.12:8077${this.prev_page_url}`)
        .then((response) => {
          this.products = response.data.data;
          this.total = response.data.total;
          this.next_page_url = response.data.next_page_url;
          this.prev_page_url = response.data.prev_page_url;
          this.prev_page = "Previous Page";
        });
    },
    async first() {
      await this.$axios
        .get(
          `http://192.168.1.12:8077${this.first_page}`
        )
        .then((response) => {
          this.products = response.data.data;
          this.total = response.data.total;
          this.next_page_url = response.data.next_page_url;
          this.prev_page_url = response.data.prev_page_url;
        });
    },
    async last() {
      await this.$axios
        .get(
          `http://192.168.1.12:8077${this.last_page}`
        )
        .then((response) => {
          this.products = response.data.data;
          this.total = response.data.total;
          this.next_page_url = response.data.next_page_url;
          this.prev_page_url = response.data.prev_page_url;
        });
    },
  },
};
</script>
