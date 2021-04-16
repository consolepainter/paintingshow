<template>
  <div class="svg">
    <div class="logo2">
      <svg width="100%" height="100%" viewBox="0 0 200 200">
        <path d="M40 0 L160 0 Q200 0 200 40 L200 160 Q200 200 160 200 L40 200 Q0 200 0 160 L0 40 Q0 0 60 0Z" fill="#000"/>
        <path d="M40 40 H120 V120 H40 Z" fill="#FFC700"/>
        <path d="M80 80 H160 V160 H80 Z" fill="#6ED47C"/>
        <path d="M80 80 H120 V120 H80 Z" fill="#BC3697"/>
      </svg>
    </div>
    <div class="logo2">
      <svg width="100%" height="100%" viewBox="0 0 200 200">
        <circle cx="100" cy="100" r="92" stroke="#000" stroke-width="5" fill="none"/>
        <path d="M100 50 H130 C160 50 160 100 130 100 H100 100Z" fill="#BC3697"/>
        <path d="M100 100 H150 V130 C150 160 100 160 100 130Z" fill="#000"/>
        <path d="M100 100 H70 C40 100 40 150 70 150 H100Z" fill="#FFC6E3"/>
        <path d="M100 100 V70 C100 40 50 40 50 70 V100Z" fill="#000"/>
      </svg>
    </div>
    <div></div>
  </div>
</template>

<script>
export default {

}
</script>

<style lang="scss" scoped>
.svg {
  display: flex;
  width: 100%;
  height: 100%;
  padding: 20px;
}
.logo1 { 
  width: 20%;
  height: 50%;
  margin-right: 20px;
  background: #eee;
}
.logo2 { 
  width: 20%;
  height: 40%;
  margin-right: 20px;
  background: #eee;
}

</style>