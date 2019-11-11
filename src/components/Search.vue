<template>
  <form class="search">
    <input
       type="text"
       :value="movieTitle"
       @keyup="handleChange"
    />
    <input @click="handleSubmit" type="submit" value="SEARCH" />
  </form>
</template>

<script>
import { ref } from '@vue/composition-api';

export default {
  name: 'Search',
  props: ['search'],
  setup({ search }, { emit }) {
    const movieTitle = ref(search);

    const handleSubmit = evt => {
      evt.preventDefault();
      emit('search', movieTitle.value);
    };

    const handleChange = evt => {
      movieTitle.value = evt.target.value;
    };

    return {
      movieTitle,
      handleSubmit,
      handleChange,
    };
  },
};
</script>
