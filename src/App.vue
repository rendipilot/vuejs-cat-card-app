<template>
  <div class="w-full h-14 flex bg-gradient-to-r from-yellow-400 to-yellow-600">
    <h3 class="text-2xl text-black w-max ml-4 my-auto font-bold">Cat World</h3>
  </div>

  <div class="flex">
    <div class=" my-10 w-11/12 mx-auto">
      <button
        @click="catFunction"
        class="bg-blue-500 p-3 rounded text-white font-semibold"
      >
      {{ isShowing ? 'Hide' : 'Show cat' }}
      </button>
      <div class="mt-5 grid grid-cols-4 gap-4">
        <CatCard v-for="(cat, index) in cats" :key="index" :imageUrl="cat.url" />
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent, ref } from "vue";
import CatCard from "./components/CatCard.vue";

export default defineComponent({
  components: {
    CatCard
  },
  setup() {
    const cats = ref([]);
    const isShowing = ref(false);


    const fetchCats = async () => {
      try {
        const res = await fetch(
          "https://api.thecatapi.com/v1/images/search?limit=10"
        );
        const data = await res.json();

        cats.value = data;
      } catch (error) {
        console.error("Error fetching cat data:", error);
      }
    };

    const catFunction = () => {
      if (isShowing.value){
          cats.value = []
      }else{
        fetchCats()
      }

      isShowing.value = !isShowing.value
    }

    return {
      cats,
      catFunction,
      isShowing,
    };
  },
});
</script>
