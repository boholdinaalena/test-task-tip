<script setup></script>

<template>
  <div class="vue">
    <div class="main">
      <div class="main__amount amount">
        <div class="amount__header title">Glad you enjoyed it today</div>
        <p class="amount__text">
          Choose the amount you wish to tip and we will transfer it directly
        </p>
        <input
          type="text"
          placeholder="Tip amount"
          class="amount__input input-text"
          v-model="tipAmount"
        />
        <form>
          <div class="amount__column column">
            <lable>
              <input
                type="radio"
                class="column__price radio"
                value="2"
                name="price"
                v-model="tipAmount"
              />
              <span class="column__price">2€</span>
            </lable>
            <label>
              <input
                type="radio"
                class="column__price radio"
                value="5"
                :checked="true"
                name="price"
                v-model="tipAmount"
              />
              <span class="column__price">5€</span>
            </label>
            <label>
              <input
                type="radio"
                class="column__price radio"
                value="10"
                name="price"
                v-model="tipAmount"
              />
              <span class="column__price">10€</span>
            </label>
          </div>
        </form>
        <!-- <hr class="amount__line line" /> -->
      </div>
      <div class="main_rate rate">
        <p class="rate__header title">Rate your experience</p>
        <StarRating @openRateToday="openRateToday" />
      </div>

      <div class="main_rate-today rate-today" v-if="visiable">
        <p class="rate-today__header title">How was your experience today?</p>
        <StarRating />
        <p class="rate-today__question">What did you enjoy the most?</p>
        <div class="rate-today__params params">
          <div class="params__counter">
            <input
              class="params__check check"
              type="checkbox"
              v-model="answers"
              value="Service"
            />
            <p class="params__text">Service</p>
          </div>
          <div class="params__counter">
            <input
              class="params__check check"
              type="checkbox"
              v-model="answers"
              value="Cleanliness"
            />
            <p class="params__text">Cleanliness</p>
          </div>
          <div class="params__counter">
            <input
              class="params__check check"
              type="checkbox"
              v-model="answers"
              value="Atmosphere"
            />
            <p class="params__text">Atmosphere</p>
          </div>
          <div class="params__counter">
            <input
              class="params__check check"
              type="checkbox"
              v-model="answers"
              value="Food quality"
            />
            <p class="params__text">Food quality</p>
          </div>
        </div>
        <div class="rate-today__description-container">
          <p class="rate-today__description description">
            High quality service and food was truly magnificent 😍🔥
          </p>
        </div>
      </div>

      <Payment
        :answers="answers"
        :tipAmount="tipAmount"
        @returnAmount="returnAmount"
      />

      <div class="main_tip tip">
        <p class="tip__header title">How much do you want to tip?</p>
        <input
          type="text"
          placeholder="Tip amount"
          class="amount__input input-text"
          v-model="payAmount"
        />
        <form>
          <div class="amount__column column">
            <lable>
              <input
                type="radio"
                class="column__price radio"
                value="2"
                name="price"
                v-model="payAmount"
              />
              <span class="column__price">2€</span>
            </lable>
            <label>
              <input
                type="radio"
                class="column__price radio"
                value="5"
                :checked="true"
                name="price"
                v-model="payAmount"
              />
              <span class="column__price">5€</span>
            </label>
            <label>
              <input
                type="radio"
                class="column__price radio"
                value="10"
                name="price"
                v-model="payAmount"
              />
              <span class="column__price">10€</span>
            </label>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import StarRating from "./components/StarRating.vue";
import Payment from "./components/Payment.vue";

export default {
  name: "vue",
  components: {
    StarRating,
    Payment,
  },
  data() {
    return {
      payAmount: 5,
      tipAmount: 5,
      visiable: false,
      answers: [],
      percentPay: 1,
    };
  },
  methods: {
    openRateToday() {
      this.visiable = true;
    },
    returnAmount(num) {
      console.log(num);
      this.percentPay = num;
      this.tipAmount = this.payAmount;
      let good_num = Number(this.payAmount * num).toFixed(2);
      this.payAmount = good_num;
    },
  },
  watch: {
    tipAmount(value) {
      if (this.percentPay == 1) {
        this.payAmount = value;
      } else {
        this.payAmount = Number(value * this.percentPay).toFixed(2);
      }
    },
    payAmount(value) {
      if (this.percentPay == 1) {
        this.tipAmount = value;
      } 
    },
  },
};
</script>
