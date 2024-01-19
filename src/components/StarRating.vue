<template>
  <div class="star-rating">
    <span class="star star__yellow" 
          v-for="i in rating" 
          :key="i"
          @click="changeRating(i)"></span>
    <span class="star star__empty" 
          v-for="j in starLimit - rating" 
          :key="j"
          @click="changeRating(j+rating)">
    </span>
  </div>
</template>
<script>
export default {
  name: "star-rating",
  data() {
    return {
        rating: 0,
        starLimit: 5
    }
  },
  methods: {
    changeRating(index) {
        this.rating = index;
        this.$emit("openRateToday");
    },
  },
};
</script>
<style lang="scss">
@import url(../assets/style.scss);

.star-rating {
  display: flex;
  justify-content: space-between;
  width: var(--text-width);
  height: 60px;
}

.star__empty {
  background: url(../assets/img/star-empty.svg);
  background-size: contain;
  background-repeat: no-repeat;
  width: 50px;
  cursor: pointer;
}
.star__yellow {
  background: url(../assets/img/star-yellow.svg);
  background-size: contain;
  background-repeat: no-repeat;
  width: 50px;
  cursor: pointer;
}
</style>
