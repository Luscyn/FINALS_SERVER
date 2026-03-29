<template>
  <div class="fetched-data-section">
    <h2 class="center">Meet Our Partners in Tech</h2>
    <p class="center mt-s large mb-l">
      Discover the advanced technology that powers our diagnostic services.
    </p>
    <div v-if="loading">Loading...</div>
    <div v-if="partners.length" class="fetched-data-grid">
      <div
        class="fetched-data-box"
        v-for="partner in partners"
        :key="partner._id"
      >
        <div>
          <img
            :src="require(`@/assets/images/partners/${partner.image}`)"
            alt="Partners Image"
          />
          <h3 class="mt-s">{{ partner.name }}</h3>
        </div>

        <p>{{ partner.description }}</p>
      </div>
    </div>
    <div v-else>No partners found.</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      partners: [
        { _id: 1, name: "Asya Medika", description: "Leading distributor of medical laboratory equipment and reagents across the Philippines.", image: "asya-medika.webp" },
        { _id: 2, name: "BioSystems", description: "Global manufacturer of clinical chemistry and immunoassay analyzers for diagnostic laboratories.", image: "biosystems.webp" },
        { _id: 3, name: "Indoplas Philippines", description: "Premier supplier of medical disposables, laboratory consumables, and healthcare products.", image: "indoplas-philippines.webp" },
        { _id: 4, name: "Macromed Philippines", description: "Trusted provider of advanced diagnostic instruments and laboratory automation solutions.", image: "macromed-philippines.webp" },
        { _id: 5, name: "MeDev Medical Devices", description: "Specialized in innovative medical devices and point-of-care diagnostic technologies.", image: "medev-medical-devices.webp" },
      ],
      loading: false,
    };
  },
};
</script>

<style scoped></style>
