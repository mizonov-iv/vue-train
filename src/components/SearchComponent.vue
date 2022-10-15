<template>
  <div class="center">
    <h1>Search Component</h1>
    <input
        type="text"
        placeholder="Текущая кредитная организация"
        v-model="searchQuery"
        @focus="searchResultsVisible = true"
        @blur="searchResultsVisible = false"
        @keyup.esc="searchResultsVisible = false"
        @input="fetchBanks"
        @keydown.up.prevent="highLightPrevious"
        @keydown.down.prevent="highLightNext"
        @keydown.enter="emit"
    >
    <div v-if="searchQuery.length > 0 && searchResultsVisible" style="max-height: 32rem">
      <div
          v-for="(bank, index) in banks"
          :key="index"
          @mousedown.prevent="searchResultsVisible = true"
          class="results"
          :class="{'highLighted': index == highLightedIndex}"
      >
        {{ bank }}
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data: () => ({
    searchQuery: '',
    searchResultsVisible: false,
    banks: [],
    highLightedIndex: 0
  }),
  methods: {
    fetchBanks() {
      this.searchResultsVisible = true
      axios.get(`http://192.168.1.135:8080/api/banks?query=${this.searchQuery}`)
          .then((response) => {
            this.banks = response.data.banks
            console.log(this.banks)
          })
          .catch(error => {
            console.log(error)
          })
    },
    highLightPrevious() {
      if(this.highLightedIndex > 0) {
        this.highLightedIndex = this.highLightedIndex - 1
      }
    },
    highLightNext() {
      if(this.highLightedIndex <= this.banks.length - 1) {
        this.highLightedIndex = this.highLightedIndex + 1
      }
    },
  }
}
</script>

<style scoped>
  .center {
    width: 600px;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }

  .results {
    width: 250px;
    border: 1px solid black;
  }

  .highLighted {
    border: 2px solid red;
  }
</style>