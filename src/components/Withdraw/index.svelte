<script lang="ts">
  import CNDSaleABI from '@/abi/CNDV2Sale.json'
  import { myAddress, signer } from '@/stores'
  import { ethers } from 'ethers'

  let confirm = false
  let CNDSale = '0x841A63491027b3cffBDBC748AB98D8a7944eb197'

  async function withdraw() {
    const contract = new ethers.Contract(CNDSale, CNDSaleABI, $signer)
    const transaction = await contract.withdraw()
    await transaction.wait()
    confirm = true
  }
</script>

<div>내 지갑주소: {$myAddress}</div>

<div class="btn" on:click="{withdraw}">정산하기</div>

{#if confirm}
  <div class="confirm">완료되었습니다.</div>
{/if}

<style>
  .withdraw {
    width: 200px;
    height: 100px;
    background: blue;
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
</style>
