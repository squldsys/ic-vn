<script setup>
const props = defineProps({
  page: {
    type: Number,
    required: true,
  },
  itemsPerPage: {
    type: Number,
    required: true,
  },
  totalItems: {
    type: Number,
    required: true,
  },
  data: {
    type: Boolean,
    required: false,
  },
});

const emit = defineEmits(["update:page"]);

const updatePage = (value) => {
  emit("update:page", value);
};
// const itemsPerPageOptions = [
//   { value: 5, title: "5件表示" },
//   { value: 10, title: "10件表示" },
//   { value: 15, title: "15件表示" },
//   { value: 20, title: "20件表示" },
// ];

// const selectedItemsPerPage = ref(props.itemsPerPage);

// const updateItemsPerPage = (value) => {
//   emit("update:itemsPerPage", value);
// };
// watch(selectedItemsPerPage, (newVal) => {
//   updateItemsPerPage(newVal);
// });
// watch(
//   () => props.data,
//   (newVal, oldVal) => {
//     console.log("data changed:", newVal);
//   },
//   { immediate: true }
// );
</script>

<template>
  <div>
    <VDivider v-if="!data" />

    <div class="d-flex align-center justify-end flex-wrap gap-3 px-6 py-3">
      <!-- <template v-if="data">
        <span class="text-h6" style="font-weight: 300"
          >合計250件（1-30件表示）
        </span>
      </template>
      <template v-if="data">
        <VSelect
          v-model="selectedItemsPerPage"
          :items="itemsPerPageOptions"
          class="my-custom-select"
        />
      </template> -->
      <p v-if="!data" class="text-disabled mb-0">
        {{ paginationMeta({ page, itemsPerPage }, totalItems) }}
      </p>

      <VPagination
        :model-value="page"
        active-color="primary"
        :length="Math.ceil(totalItems / selectedItemsPerPage)"
        :total-visible="
          $vuetify.display.xs
            ? 1
            : Math.min(Math.ceil(totalItems / selectedItemsPerPage), 5)
        "
        @update:model-value="updatePage"
      />
    </div>
  </div>
</template>
<style scoped>
.my-custom-select .v-select__selections {
  height: 40px; /* Thay đổi chiều cao */
}

.my-custom-select .v-select__control {
  width: 200px; /* Thay đổi chiều rộng */
}
</style>
