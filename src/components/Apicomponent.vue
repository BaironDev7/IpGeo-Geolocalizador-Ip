<template>
  <div class="bg-blue-700 h-screen flex items-center justify-center">
    <div
      class="bg-white rounded-lg shadow-md mx-auto p-6 w-full max-w-2xl flex justify-center flex-col"
    >
    <h2 class="text-center text-2xl font-semibold mb-4">Geolocalización con IpGeo</h2>
      <div class="flex h-10 justify-center">
        <input
          type="text"
          v-model="ipAddress"
          class="border border-gray-300 p-2 mr-2"
          placeholder="Ingrese una dirección IP"
        />
        <button
          @click="fetchIpData"
          class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
        >
          Buscar
        </button>
      </div>
      <div v-if="ipData" class="mt-4 flex justify-between">
        <div class="ml-10">
          <p><strong>IP:</strong> {{ ipData.ip }}</p>
          <p><strong>Tipo:</strong> {{ ipData.type }}</p>
          <p><strong>Continente:</strong> {{ ipData.continent_name }}</p>
          <p><strong>País:</strong> {{ ipData.country_name }}</p>
          <p><strong>Capital:</strong> {{ ipData.location.capital }}</p>
          <p><strong>Estado:</strong> {{ ipData.region_name }}</p>
          <p><strong>Ciudad:</strong> {{ ipData.city }}</p>
          <p><strong>Latitud:</strong> {{ ipData.latitude }}</p>
          <p><strong>Longitud:</strong> {{ ipData.longitude }}</p>
          <p>
            <strong>Idioma:</strong> {{ ipData.location.languages[0].name }}
          </p>
          <p>
            <strong>Código de llamadas:</strong>
            {{ ipData.location.calling_code }}
          </p>
        </div>

        <div class="mr-10 mt-10">
          <p class="text-9xl">{{ ipData.location.country_flag_emoji }}</p>
          <p class="text-center font-semibold">Bandera:</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      ipAddress: "",
      ipData: null,
    };
  },
  methods: {
    async fetchIpData() {
      try {
        const response = await axios.get(
          `http://api.ipstack.com/${this.ipAddress}?access_key=6b3232d816b873436f23e558354f2ff2`
        );
        this.ipData = response.data;
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>
