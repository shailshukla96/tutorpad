<template>
  <div>
    <h3 class="mb-2">{{ title }}</h3>

    <div class="flex flex-wrap -mx-2">
      <div
        class="w-1/2 sm:w-1/3 md:w-1/4 lg:w-1/4 p-2"
        v-for="(item, i) in items"
        :key="i"
      >
        <finder-group-item
          :item="item"
          :is-active="selected.includes(i)"
          @select="handleSelect(i)"
          @deselect="handleDeselect(i)"
        />
      </div>
    </div>
  </div>
</template>

<script>
import FinderGroupItem from './FinderGroupItem.vue';
export default {
  name: 'FinderGroup',
  components: {
    FinderGroupItem,
  },
  props: {
    title: {
      type: String,
      required: true,
    },
    items: {
      type: Array,
      required: true,
    },
    selected: {
      type: Array,
      required: true,
    },
  },
  methods: {
    handleSelect(index) {
      this.$emit('update', [...this.selected, index]);
    },
    handleDeselect(index) {
      this.$emit('update', this.selected.filter(i => i !== index));
    },
  },
};
</script>