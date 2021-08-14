<template>
  <table class="table table-dark">
    <thead>
      <tr>
        <th v-for="title in titles" :key="title">{{ title }}</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(coin, index) in coinsFilter" :key="coin.id">
        <td>{{ index + 1 }}</td>
        <td>
          <img :src="coin.image" style="width: 2rem" class="me-2" />
          <span>
            {{ coin.name }}
          </span>
          <span class="ms-2 text-uppercase text-muted">
            {{ coin.symbol }}
          </span>
        </td>
        <td>$ {{ coin.current_price }}</td>
        <td
          :class="[
            coin.price_change_percentage_24h > 0
              ? 'text-success'
              : 'text-danger',
          ]"
        >
          {{ coin.price_change_percentage_24h }} %
        </td>
        <td>$ {{ coin.total_volume.toLocaleString() }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: "Table",
  props: {
    coinsFilter: Array,
  },
};
</script>