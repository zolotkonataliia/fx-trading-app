<template>
  <div class="rate-panel">
    <h2 class="rate-panel__title">{{ rate.pair }}</h2>
    <div class="rate-panel__content">
      <div class="rate-panel__sell">
        <div class="rate-panel__sell__inner">
          <strong class="rate-panel__sell__title">Sell {{ rate.pair.substr(0, 3) }}</strong>
          <span class="rate-panel__sell__text">
            {{ rate.sell.toString().substr(0, 4) }}<strong>{{ rate.sell.toString().substr(-3, 2)}}</strong><sup>{{ rate.sell.toString().substr(-1, 1)}}</sup>
          </span>
        </div>
      </div>
      <div class="rate-panel__buy">
        <div class="rate-panel__buy__inner">
          <strong class="rate-panel__buy__title">Buy {{ rate.pair.substr(0, 3) }}</strong>
          <span class="rate-panel__sell__text">
            {{ rate.buy.toString().substr(0, 4) }}<strong>{{ rate.buy.toString().substr(-3, 2)}}</strong><sup>{{ rate.buy.toString().substr(-1, 1)}}</sup>
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    rate: {
      type: Object,
      required: true
    }
  }
}
</script>

<style lang="scss" scoped>
.rate-panel {
  margin: 0 0 10px;
  background-color: #f2fbff;
  border: 1px solid #b4b4b3;
  -webkit-flex: 0 1 97px;
  -ms-flex: 0 1 97px;
  flex: 0 1 97px;
  max-width: 253px;
  min-width: 250px;

  @media screen and (min-width: 768px) {
    -webkit-flex: 0 1 253px;
    -ms-flex: 0 1 253px;
    flex: 0 1 253px;
    margin: 1%;
  }

  &__title {
    color: #fff;
    text-transform: uppercase;
    background-color: #595959;
    padding: 3px;
    border-bottom: 1px solid #444443;
    text-align: center;
    margin: 0;
    font-size: 14px;
    line-height: 1.2;
  }
  &__content {
    padding: 4px 10px;
    min-height: 75px;
    overflow: hidden;
    position: relative;
    &:after {
      content: '';
      position: absolute;
      left: 50%;
      top: 4px;
      width: 0;
      height: 0;
      margin-left: -4px;
      border-left: 5px solid transparent;
      border-right: 5px solid transparent;
      border-bottom: 12px solid green;
      .decreased & {
        border-left: 5px solid transparent;
        border-right: 5px solid transparent;
        border-top: 12px solid red;
        border-bottom: none;
      }
    }
  }
  &__sell,
  &__buy {
    float: left;
    width: 48%;
    min-width: 110px;
    height: 41px;
    position: relative;
    color: red;
    &__inner {
      background-color: #fff;
      border: solid #d3d4d4;
      border-width: 1px 0 1px 1px;
      width: 80%;
      height: 100%;
      position: relative;
      z-index: 20;
      padding: 4px;
    }
    &__title {
      font-size: 10px;
      display: block;
    }
    &__text {
      strong {
        font-size: 18px;
      }
    }
    &:after {
      content: "";
      position: absolute;
      z-index: 10;
      right: 7px;
      top: 6px;
      width: 30px;
      height: 29px;
      background-color: #fff;
      border: solid #d3d4d4;
      border-width: 1px 1px 0 0;
      transform: rotate(45deg);
      border-radius: 0 10px 0 0;
    }
  }
  &__buy {
    float: right;
    text-align: right;
    color: green;
    &__inner {
      border-width: 1px 1px 1px 0;
      float: right;
    }
    &:after {
      left: 7px;
      right: auto;
      border-width: 0 0 1px 1px;
      border-radius: 0 0 0 10px;
      height: 30px;
    }
  }
}
</style>
