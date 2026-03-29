<template>
  <div class="fetched-data-section">
    <h2 class="center">Find The Service You're Looking For!</h2>
    <p class="center mt-s large mb-l">
      Explore Our Comprehensive Range of Diagnostic Tests to Support Your Health
      Needs.
    </p>

    <p class="center">
      <input
        type="text"
        v-model="searchQuery"
        placeholder="Search for a service..."
        @input="filterServices"
        class="search-input"
      />
    </p>

    <div v-if="loading">Loading...</div>
    <div v-if="Object.keys(groupedServices).length">
      <div
        v-for="(serviceGroup, category) in groupedServices"
        :key="category"
        class="mt-l"
      >
        <h3>{{ category }}</h3>
        <div class="fetched-data-grid">
          <div
            v-for="service in serviceGroup"
            :key="service._id"
            class="fetched-data-box"
          >
            <div>
              <img
                :src="require(`@/assets/images/services/${service.image}`)"
                alt="Service Image"
              />
              <h3 class="mt-s">{{ service.name }}</h3>
            </div>

            <div>
              <p>{{ service.description }}</p>
              <p class="aqua right mt-s">Php {{ service.price }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div v-else>No services found.</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      services: [
        { _id: 1, name: "Complete Blood Count (CBC)", description: "A comprehensive blood test that evaluates overall health and detects a wide range of disorders including anemia, infection, and leukemia.", price: 350, category: "Hematology", image: "complete_blood_count.webp" },
        { _id: 2, name: "Hemoglobin Test", description: "Measures the amount of hemoglobin in your blood to check for conditions such as anemia or polycythemia.", price: 200, category: "Hematology", image: "hemoglobin_test.webp" },
        { _id: 3, name: "Platelet Count", description: "Determines the number of platelets in your blood to assess clotting ability and detect bleeding disorders.", price: 250, category: "Hematology", image: "platelet_count.webp" },
        { _id: 4, name: "Reticulocyte Count", description: "Measures immature red blood cells to evaluate bone marrow function and response to anemia treatment.", price: 300, category: "Hematology", image: "reticulocyte_count.webp" },
        { _id: 5, name: "Blood Sugar Test", description: "Measures glucose levels in the blood to screen for diabetes and monitor blood sugar control.", price: 150, category: "Clinical Chemistry", image: "blood_sugar_test.webp" },
        { _id: 6, name: "HbA1c", description: "Provides an average blood sugar level over the past 2-3 months, essential for diabetes management.", price: 500, category: "Clinical Chemistry", image: "hba1c.webp" },
        { _id: 7, name: "Lipid Profile", description: "Measures cholesterol and triglycerides to assess cardiovascular risk and guide treatment plans.", price: 600, category: "Clinical Chemistry", image: "lipid_profile.webp" },
        { _id: 8, name: "Liver Function Test", description: "Evaluates how well the liver is working by measuring enzymes, proteins, and bilirubin levels.", price: 550, category: "Clinical Chemistry", image: "liver_function_test.webp" },
        { _id: 9, name: "Creatinine Test", description: "Assesses kidney function by measuring creatinine levels in the blood.", price: 250, category: "Clinical Chemistry", image: "creatinine_test.webp" },
        { _id: 10, name: "Metabolic Panel", description: "A group of tests that measure electrolytes, glucose, and kidney markers to evaluate metabolic function.", price: 700, category: "Clinical Chemistry", image: "metabolictest.webp" },
        { _id: 11, name: "Thyroid Function Test", description: "Measures thyroid hormones (TSH, T3, T4) to diagnose thyroid disorders and monitor treatment.", price: 800, category: "Immunology & Serology", image: "thyroid_function_test.webp" },
        { _id: 12, name: "Insulin Test", description: "Measures insulin levels to help diagnose insulin resistance, diabetes, and hypoglycemia.", price: 650, category: "Immunology & Serology", image: "InsulinTest.webp" },
        { _id: 13, name: "Estrogen Test", description: "Evaluates estrogen hormone levels for reproductive health assessment and fertility monitoring.", price: 750, category: "Immunology & Serology", image: "estrogen_test.webp" },
        { _id: 14, name: "Testosterone Test", description: "Measures testosterone levels to assess hormonal balance and reproductive health.", price: 700, category: "Immunology & Serology", image: "testosterone_test.webp" },
        { _id: 15, name: "Prolactin Test", description: "Measures prolactin hormone levels to evaluate pituitary gland function and fertility issues.", price: 600, category: "Immunology & Serology", image: "prolactin_test.webp" },
        { _id: 16, name: "Urinalysis", description: "A complete urine examination to detect urinary tract infections, kidney disease, and diabetes.", price: 200, category: "Urinalysis", image: "urinalysis.webp" },
        { _id: 17, name: "Urine Culture", description: "Identifies bacteria in urine to diagnose urinary tract infections and determine appropriate antibiotics.", price: 450, category: "Urinalysis", image: "UrineCulture.webp" },
        { _id: 18, name: "Random Urine Test", description: "A spot urine collection for quick screening of kidney function and metabolic conditions.", price: 180, category: "Urinalysis", image: "random_urine_test.webp" },
        { _id: 19, name: "Microalbumin Test", description: "Detects small amounts of albumin in urine, an early indicator of kidney damage especially in diabetics.", price: 400, category: "Urinalysis", image: "microalbumin_test.webp" },
        { _id: 20, name: "24-Hour Urine Protein Test", description: "Collects urine over 24 hours to measure total protein output and assess kidney health.", price: 500, category: "Urinalysis", image: "24h_urine_protein_test.webp" },
        { _id: 21, name: "Chest X-Ray", description: "Produces images of the heart, lungs, and chest wall to diagnose respiratory and cardiac conditions.", price: 400, category: "Imaging", image: "chest_xray.webp" },
        { _id: 22, name: "Ultrasound", description: "Uses sound waves to produce images of internal organs for non-invasive diagnostic evaluation.", price: 1200, category: "Imaging", image: "ultrasound.webp" },
        { _id: 23, name: "CT Scan", description: "Combines X-ray images taken from different angles to create cross-sectional views of bones, blood vessels, and soft tissues.", price: 3500, category: "Imaging", image: "ct_scan.webp" },
        { _id: 24, name: "MRI", description: "Uses magnetic fields and radio waves to generate detailed images of organs and tissues for advanced diagnostics.", price: 5000, category: "Imaging", image: "mri.webp" },
      ],
      loading: false,
      searchQuery: "",
    };
  },
  computed: {
    filteredServices() {
      if (!this.searchQuery) {
        return this.services;
      }
      const query = this.searchQuery.toLowerCase();
      return this.services.filter(
        (service) =>
          service.name.toLowerCase().includes(query) ||
          service.description.toLowerCase().includes(query)
      );
    },
    groupedServices() {
      return this.filteredServices.reduce((groups, service) => {
        const category = service.category;
        if (!groups[category]) {
          groups[category] = [];
        }
        groups[category].push(service);
        return groups;
      }, {});
    },
  },
};
</script>

<style scoped></style>
