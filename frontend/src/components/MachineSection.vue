<template>
  <div class="fetched-data-section">
    <h2>Our Machines</h2>
    <p class="mt-s large mb-l">
      State-of-the-art equipment for precise and reliable results.
    </p>
    <div v-if="loading">Loading...</div>
    <div v-if="machines.length">
      <div
        v-for="(machineGroup, category) in groupedMachines"
        :key="category"
        class="mt-l"
      >
        <h3 class="">{{ category }}</h3>
        <div class="fetched-data-grid">
          <div
            v-for="machine in machineGroup"
            :key="machine._id"
            class="fetched-data-box"
          >
            <div>
              <img
                :src="require(`@/assets/images/machines/${machine.image}`)"
                alt="Machine Image"
              />
              <h3 class="mt-s">{{ machine.name }}</h3>
            </div>

            <p>{{ machine.description }}</p>
          </div>
        </div>
      </div>
    </div>
    <div v-else>No machines found.</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      machines: [
        { _id: 1, name: "Hematology Analyzer", description: "Automated blood cell counter that performs complete blood count analysis with high precision and speed.", category: "Hematology", image: "hematology-analyzer.webp" },
        { _id: 2, name: "Blood Smear Machine", description: "Prepares uniform blood smear slides for microscopic examination of blood cell morphology.", category: "Hematology", image: "blood-smear-machine.webp" },
        { _id: 3, name: "Centrifuge Machine", description: "Separates blood components by spinning samples at high speed for serum and plasma preparation.", category: "Hematology", image: "centrifuge-machine.webp" },
        { _id: 4, name: "Microscope", description: "High-powered optical microscope for detailed examination of blood smears, urine sediment, and tissue samples.", category: "General Laboratory", image: "microscope.webp" },
        { _id: 5, name: "Serology Analyzer", description: "Automated system for detecting antibodies and antigens to diagnose infectious diseases and immune disorders.", category: "Immunology & Serology", image: "serology-analyzer.webp" },
        { _id: 6, name: "ELISA Plate Reader", description: "Reads enzyme-linked immunosorbent assay plates for quantitative detection of proteins, hormones, and antibodies.", category: "Immunology & Serology", image: "elisa-plate-reader.webp" },
        { _id: 7, name: "PCR Machine", description: "Polymerase chain reaction thermal cycler for molecular diagnostics and DNA amplification.", category: "Molecular Diagnostics", image: "pcr-machine.webp" },
        { _id: 8, name: "Blood Typing Kit", description: "Standardized reagent kit for ABO and Rh blood group determination.", category: "Blood Banking", image: "blood-typing-kit.webp" },
        { _id: 9, name: "Urine Analyzer", description: "Automated urine chemistry analyzer for rapid and accurate urinalysis testing.", category: "Urinalysis", image: "urine-analyzer.webp" },
        { _id: 10, name: "Urine Strip Reader", description: "Digital reader for urine reagent strips providing standardized and objective test results.", category: "Urinalysis", image: "urine-strip-reader.webp" },
        { _id: 11, name: "Urinalysis Centrifuge", description: "Specialized centrifuge for urine sediment preparation and microscopic analysis.", category: "Urinalysis", image: "urinalysis-centrifuge.webp" },
        { _id: 12, name: "Refractometer", description: "Measures urine specific gravity to assess kidney concentrating ability.", category: "Urinalysis", image: "refractometer.webp" },
        { _id: 13, name: "HIV Rapid Test Kit", description: "Point-of-care diagnostic kit for rapid screening of HIV antibodies with results in minutes.", category: "Rapid Test Kits", image: "hiv-rapid-test-kit.webp" },
        { _id: 14, name: "Typhoid Test Kit", description: "Rapid diagnostic test for detection of Salmonella typhi antibodies in patient serum.", category: "Rapid Test Kits", image: "typhoid-test-kit.webp" },
        { _id: 15, name: "Micral Test Kit", description: "Quantitative test strip for microalbumin detection in urine for early kidney damage screening.", category: "Rapid Test Kits", image: "micral-test-kit.webp" },
      ],
      loading: false,
    };
  },
  computed: {
    groupedMachines() {
      return this.machines.reduce((groups, machine) => {
        const category = machine.category;
        if (!groups[category]) {
          groups[category] = [];
        }
        groups[category].push(machine);
        return groups;
      }, {});
    },
  },
};
</script>

<style scoped></style>
