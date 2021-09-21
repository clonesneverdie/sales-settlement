<script lang="ts">
  import CNDSaleABI from '@/abi/CNDV2Sale.json'
  import { myAddress, signer } from '@/stores'
  import { ethers } from 'ethers'
  import { onMount } from 'svelte'

  const provider = new ethers.providers.JsonRpcProvider('https://polygon-rpc.com/')
  onMount(() => {
    income()
  })
  let balance: any
  let c1: any
  let c2: any
  let c3: any
  let confirm = false
  let CNDSale = '0x841A63491027b3cffBDBC748AB98D8a7944eb197'

  async function income() {
    balance = await provider.getBalance(CNDSale)
    balance = balance / 1e18
    c1 = (balance / 100) * 25
    c2 = (balance / 100) * 38
    c3 = (balance / 100) * 37
  }

  async function withdraw() {
    const contract = new ethers.Contract(CNDSale, CNDSaleABI, $signer)
    const transaction = await contract.withdraw()
    await transaction.wait()
    confirm = true
  }
</script>

<div>
  미정산 매틱: {balance}
</div>
<div>
  C1: {c1}
</div>
<div>
  C2: {c2}
</div>
<div>
  C3: {c3}
</div>

<div>내 지갑주소: {$myAddress}</div>

<div class="btn" on:click="{withdraw}">정산하기</div>

{#if confirm}
  <div class="confirm">완료되었습니다.</div>
{/if}

<style>
  .btn {
    width: 20%;
    background-color: tomato;
    font-size: 20px;
    border-radius: 10px;
    text-align: center;
    padding: 10px;
    box-sizing: border-box;
    cursor: pointer;
  }

  @media screen and (max-width: 768px) {
    .btn {
      width: 50%;
      background-color: tomato;
      font-size: 20px;
      border-radius: 10px;
      text-align: center;
      padding: 10px;
      box-sizing: border-box;
      cursor: pointer;
      margin-top: 10px;
    }
  }
</style>
