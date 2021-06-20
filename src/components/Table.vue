<template>
  <v-data-table
    :headers="headers"
    :items="items"
    :items-per-page="5"
    class="elevation-1"
  ></v-data-table>
</template>

<script>
export default {
  name: "Table",
  props: ["contents"],

  data() {
    return {
      headers: Object.keys(this.contents[0]).map((item) => ({
        text: item.charAt(0).toUpperCase() + item.slice(1),
        value: item,
      })),
      items: this.contents,
    };
  },
};
</script>
