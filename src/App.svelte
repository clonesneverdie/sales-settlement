<script lang="ts">
  import WalletConnect from '@/components/WalletConnect/index.svelte'
  import Withdraw from '@/components/Withdraw/index.svelte'
</script>

<div class="wrap">
  <div class="btn">
    <WalletConnect />
  </div>
  <Withdraw />
</div>

<style>
  .wrap {
    max-width: 1280px;
    margin: 0px auto;
  }

  .btn {
    width: 100%;
    background-color: tomato;
    font-size: 20px;
    border-radius: 10px;
    text-align: center;
    padding: 10px;
    box-sizing: border-box;
    cursor: pointer;
  }

  @media screen and (max-width: 768px) {
    .wrap {
      margin: 0px 0px;
    }
  }
</style>
