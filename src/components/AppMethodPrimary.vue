<template>
  <div>
    <label for="firstmethod">I have an array, I would like to</label>
    <select id="firstmethod" name="select" v-model="selectedFilter">
      <option value="" disabled selected>...</option>
      <option v-for="option in options" :key="option.name" :value="option">
        {{ option }}
      </option>
    </select>
    <div v-if="selectedFilter === 'add items or other arrays'">
      <method-choice :options="adding" methodType="add"/>
    </div>
    <div v-else-if="selectedFilter === 'remove items'">
      <method-choice :options="removing" methodType="remove"/>
    </div>
    <div v-else-if="selectedFilter === 'walk over items'">
      <method-choice :options="iterate" methodType="iterate by"/>
    </div>
    <div v-else-if="selectedFilter === 'find items'">

      <p>
        <label for="findmethod">I'm trying to find</label>
        <select id="findMethod" name="select" v-model="selectedFind">
          <option value="" disabled selected>...</option>
          <option value="single">one item</option>
          <option value="many">one or many items</option>
        </select>
      </p>
      
      <div v-if="selectedFind === 'single'">
        <method-choice :options="find.single" methodType="find"/>
      </div>

      <div v-else-if="selectedFind === 'many'">
        <method-choice :options="find.many" methodType="find"/>
      </div>

    </div>
    <div v-else-if="selectedFilter === 'order an array'">
      <method-choice :options="ordering"/>
    </div>
    <div v-else-if="selectedFilter === 'return a string'">
      <method-choice :options="string"/>
    </div>
    <div v-else-if="selectedFilter === 'something else'">
      <method-choice :options="other"/>
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex'
import MethodChoice from './methods/MethodChoice.vue'

export default {
  components: {
    MethodChoice
  },
  data() {
    return {
      selectedFilter: '',
      selectedFind: '',
      options: [
        'add items or other arrays',
        'remove items',
        'find items',
        'walk over items',
        'return a string',
        'order an array',
        'something else'
      ]
    }
  },
  computed: {
    ...mapState([
      'adding',
      'removing',
      'iterate',
      'string',
      'ordering',
      'other',
      'find'
    ])
  },
  watch: {
    selectedFilter() {
      this.$store.commit('resetSelection')
    },
    selectedFind() {
      this.$store.commit('resetSelection')
    }
  }
}
</script>

<style scoped>

</style>