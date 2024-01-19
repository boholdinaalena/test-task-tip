<template>
  <div class="main_pay pay">
    <div class="pay__container">
      <div class="pay__textbox">
        <p class="pay__text">I want Philip to get the full amount</p>
        <p class="pay__description description">
          You compensate service commission, and 2.27 € will be debited from
          your card.
        </p>
      </div>
      <div class="pay__switch switch" v-if="toogle" @click="toogleOn">
        <div class="switch__container">
          <div class="switch__toogle"></div>
        </div>
      </div>
      <div class="pay__switch switch-on" v-if="!toogle" @click="toogleOff">
        <div class="switch-on__container">
          <div class="switch-on__toogle"></div>
        </div>
      </div>
    </div>
    <div class="pay__apple-pay" @click="checkAnswers">
      <img
        class="pay__apple-logo"
        src="../assets/img/apple-pay.svg"
        alt="Apple Pay"
      />
    </div>
    <div class="pay__card-pay" @click="checkAnswers">Pay by card</div>
    <div class="pay__agree">
      <input type="checkbox" class="pay__check check" />
      <p class="pay__description description">
        I agree with <u>Terms & Conditions and Privacy policy</u>
      </p>
    </div>
  </div>
</template>
<script>
export default {
  name: "pay",
  props: {
    answers: Array,
  },
  data() {
    return {
      toogle: true,
      amount: this.tipAmount,
    };
  },
  methods: {
    checkAnswers() {
      if (this.answers.length != 0) {
        alert("Button active");
      }
    },
    toogleOn() {
      this.toogle = false;
      this.$emit("returnAmount", 1.1);
    },
    toogleOff() {
      this.toogle = true;
      this.$emit("returnAmount", 1);
    },
  },
};
</script>
