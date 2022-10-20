<template>
  <div>
    <!--Hero Section-->
      <div class="container px-3 mx-auto flex flex-wrap flex-col md:flex-row items-center">
        <!--Left Col-->
        <div class="flex flex-col w-full md:w-2/5 justify-center items-start text-center md:text-left">
          <h1 class="my-6 text-5xl font-bold leading-tight text-at-blue">
            Easy, Safety and Comfortable
          </h1>
          <p class="leading-normal text-2xl mb-8 text-light-black">
            Make your trip more fun with Remojo.
          </p>
        </div>
        <!--Right Col-->
        <div class="w-full md:w-3/5 text-center">
          <img class="w-full z-50" src="../assets/images/Image-Hero.svg" />
        </div>
      </div>

      <div class="bg-at-blue">
        <div class="container mx-auto flex flex-wrap flex-col md:flex-row items-center">
        <!--Left Col-->
        <div class="flex flex-col w-full md:w-2/5 justify-center items-start text-center md:text-left ">
          <h1 class="my-6 text-8xl font-bold leading-tight text-white">
            REMOJO
          </h1>
        </div>
        <!--Right Col-->
        <div class="w-full py-6 px-6 md:w-3/5 text-center">
          <h1 class="my-6 text-5xl font-bold leading-tight text-white">
            About Us
          </h1>
          <h1 class="my-6 text-2xl leading-tight text-white text-justify">
            Lorem, ipsum dolor sit amet consectetur adipisicing elit. Tempore labore similique fuga beatae aliquid quod voluptas, tempora quibusdam dolores temporibus illo repellendus eos dolorum laboriosam suscipit quis. Iusto dolore adipisci, voluptas vitae omnis harum mollitia rem laudantium iste incidunt quos!
          </h1>
          <h1 class="my-6 text-2xl leading-tight text-white text-justify">
            Lorem, ipsum dolor sit amet consectetur adipisicing elit. Tempore labore similique fuga beatae aliquid quod voluptas, tempora quibusdam dolores temporibus illo repellendus eos dolorum laboriosam suscipit quis. Iusto dolore adipisci, voluptas vitae omnis harum mollitia rem laudantium iste incidunt quos!
          </h1>
        </div>
      </div>

    <section class="bg-white border-b py-8">
      <div class="container mx-auto flex flex-wrap pt-4 pb-12">
        <h2 class="w-full my-2 text-5xl font-bold leading-tight text-center text-at-blue">
          Catalogue
        </h2>
        <ProductCard />
        <ProductCard />
        <ProductCard />
      </div>
    </section>

    <div class="container px-3 mx-auto flex flex-wrap flex-col md:flex-row items-center">
        <!--Left Col-->
        <div class="flex flex-col w-full md:w-2/5 justify-center items-start text-center md:text-left">
          <h1 class="my-6 text-5xl font-bold leading-tight text-white">
            Our Contact
          </h1>
          <p class="leading-normal text-xl mb-2 text-white">
            +628123456789
          </p>
          <p class="leading-normal text-xl mb-2 text-white">
            remojo@gmail.com
          </p>
          <p class="leading-normal text-xl mb-2 text-white">
            Jalan Kaliurang KM 2 No 49, Yogyakarta
          </p>
        </div>
        <!--Right Col-->
        <div class="w-full md:w-3/5 p-16 text-center rounded-2xl">
          <img class="w-full z-50 rounded-2xl" src="../assets/images/Yogyakarta.jpeg" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import { supabase } from "../supabase/init";
import ProductCard from "../components/ProductCard.vue";
export default {
  name: "home",
  components: { ProductCard },
  setup() {
    // Create data / vars
    const data = ref([]);
    const dataLoaded = ref(null);
    // Get data
    const getData = async () => {
      try {
        const { data: workout, error } = await supabase.from("workout").select("*");
        if (error) throw error;
        data.value = workout;
        dataLoaded.value = true;
      } catch (error) {
        console.warn(error.message); 
      }
    };
    // Run data function
    getData();
    return { data, dataLoaded };
  },
};
</script>