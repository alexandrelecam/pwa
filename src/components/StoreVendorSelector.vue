<template>
  <div class="search">
    <div class="search__box">
      <div class="search__box__icon">
        <i class="material-icons">home</i>
      </div>
      <vSelect
        class="search__box__select"
        v-if="store.stores"
        v-model="store.selectedStore"
        :options="store.stores"
        label="store_name"
        :reduce="(v) => v.store_id"
        :clearable="false"
        placeholder="concession"
        @update:modelValue="storesChange"
      />
    </div>

    <div v-if="store.vendorsList" class="search__box">
      <div class="search__box__icon">
        <!-- <i class="fa-solid fa-magnifying-glass"></i> -->
        <i class="material-icons">search </i>
      </div>
      <vSelect
        class="search__box__select"
        v-model="store.selectedVendor"
        :options="store.vendorsList"
        label="fullName"
        :reduce="(v) => v.id"
        placeholder="vendeur"
        :clearable="false"
        @update:modelValue="$emit('vendorChange')"
      />
    </div>
  </div>
</template>

<script>
import vSelect from "vue-select";
import warehouse from "../assets/photos/warehouse.svg";
import { useStore } from "../store";

export default {
  components: { vSelect },
  mounted() {},
  data() {
    return {
      store: useStore(),
      userId: "",
      user: null,
      vendors: null,
      stores: null,
      selectedVendor: null,
      selectedStore: null,
      vendorsList: null,
      error: null,
      image: warehouse,
    };
  },

  watch: {},

  methods: {
    storesChange() {
      this.store.getVendorsList();
      this.selectedVendor = null;
    },
  },
};
</script>
<style scoped lang="scss">
@import "vue-select/dist/vue-select.css";

input {
  color: var(--gray);
  background: var(--primary);
  border: none;
  outline: none;
}

.search__box {
  display: flex;

  &__select {
    height: 32px;
    width: 100%;
    background: black;
    border-radius: 0px 6px 6px 0px;
    margin-bottom: 10px;
    font-weight: 300;
  }

  &__icon {
    height: 32px;
    background: black;
    color: white;
    padding: 10px;
    border-radius: 6px 0 0 6px;
    display: flex;
    place-items: center;
  }

  &__icon img {
    height: 19px;
    display: flex;
    justify-content: center;
  }
}

.search__box__select {
  --vs-controls-color: var(--gray);
  --vs-search-input-bg: black;
  --vs-border-width: 0px;

  --vs-dropdown-bg: black;
  --vs-dropdown-color: white;
  --vs-dropdown-option-color: white;

  --vs-selected-bg: var(--purple);
  --vs-selected-color: white;

  --vs-search-input-color: white;

  --vs-dropdown-option--active-bg: var(--purple);
  --vs-dropdown-option--active-color: white;
}
</style>
