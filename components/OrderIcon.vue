<template>
  <div class="screen">
    <div class="text-wrapper">배달 오더</div>
    <div class="div">배달로 받기</div>
  </div>
</template>

<script>
export default {
  name: 'OrderIcon',
  components: {},
}
</script>

<style>
.screen {
  background-size: 100% 100%;
  height: 90px;
  position: relative;
  width: 150px;
}

.screen .text-wrapper {
  color: #000000;
  font-family: var(--title-t18-bold-font-family);
  font-size: var(--title-t18-bold-font-size);
  font-style: var(--title-t18-bold-font-style);
  font-weight: var(--title-t18-bold-font-weight);
  left: 12px;
  letter-spacing: var(--title-t18-bold-letter-spacing);
  line-height: var(--title-t18-bold-line-height);
  position: absolute;
  top: 11px;
  white-space: nowrap;
}

.screen .div {
  color: #000000;
  font-family: var(--title-t10-regular-font-family);
  font-size: var(--title-t10-regular-font-size);
  font-style: var(--title-t10-regular-font-style);
  font-weight: var(--title-t10-regular-font-weight);
  left: 12px;
  letter-spacing: var(--title-t10-regular-letter-spacing);
  line-height: var(--title-t10-regular-line-height);
  opacity: 0.5;
  position: absolute;
  top: 35px;
  white-space: nowrap;
}

.screen .ic-bike {
  height: 33px !important;
  left: 89px !important;
  position: absolute !important;
  top: 45px !important;
  width: 44px !important;
}
</style>
