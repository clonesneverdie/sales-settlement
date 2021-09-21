<script lang="ts">
  import { ethers } from 'ethers'
  import { isConnect, myAddress, signer, provider } from '@/stores'

  const ethereum: any | undefined = (window as any).ethereum

  $: if ($isConnect === true) {
    getInfo()
  }

  async function requestAccount() {
    await ethereum.request({ method: 'eth_requestAccounts' })
    $isConnect = true
  }

  async function addChain() {
    await ethereum.request({
      method: 'wallet_addEthereumChain',
      params: [
        {
          chainId: '0x89',
          chainName: 'Polygon Mainnet',
          nativeCurrency: {
            name: 'Matic',
            symbol: 'MATIC',
            decimals: 18
          },
          rpcUrls: ['https://polygon-rpc.com/'],
          blockExplorerUrls: ['https://polygonscan.com/']
        }
      ]
    })
  }

  async function getInfo() {
    $provider = new ethers.providers.Web3Provider(ethereum)
    $signer = $provider.getSigner()
    await getAddress()
  }

  async function getAddress() {
    $myAddress = await $signer.getAddress()
  }

  function changed() {
    ethereum.on('accountsChanged', async () => {
      await getAddress()
    })
  }

  async function connect() {
    if (ethereum === undefined) {
      alert('There is no Metamask. Please install Metamask.')
      return false
    }
    await addChain()
    requestAccount()
    changed()
  }
</script>

<div on:click="{connect}">
  <div class="btn">
    <b> Wallet Connect </b>
  </div>
</div>
