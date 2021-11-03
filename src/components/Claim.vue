<template>
  <div class="claimWrapper">
    <h1 class="claim">Spacer</h1>
    <p class="subclaim">
      Begin your journey trought our amazing galaxy, and discover places your
      never even heard of.
    </p>
    <p class="subclaim">Type anything space-related to start.</p>
  </div>
</template>
<script>
export default {
  // eslint-disable-next-line quotes
  name: "Claim",
};
</script>

<style lang="scss" scoped>
.claimWrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.claim {
  font-size: 50px;
  margin: 0;
}

.subclaim {
  margin: 20px 0 0 0;
  font-size: 13px;
}
</style>
