<script>
  import { fly, fade } from 'svelte/transition';
  import Info from './Info.svelte';

  let arpoja = 'Severi';

  let rivienLkm = 0;
  let maxNro = 40;
  let minNro = 1;
  let arvotut = [];

  function lisaaRivi() {
    rivienLkm++;
  }

  function nollaa() {
    rivienLkm = 0;
    arvotut = [];
    document.getElementById('hide').style.display = '';
  }

  function lottoKone() {
    if (rivienLkm > 1) {
      alert(
        'Tämän ohjelman magia riittää vain yhteen riviin, ole hyvä ja koita uudestaan!'
      );
      rivienLkm = 0;
      arvotut = [];
    } else {
      for (let kierros = 0; kierros < rivienLkm; kierros++) {
        const arvottavienLkm = 7;
        for (let kpl = 0; kpl < arvottavienLkm; kpl++) {
          const luku =
            Math.floor(Math.random() * (maxNro + 1 - minNro)) + minNro;
          if (luku !== arvotut[luku]) {
            arvotut = [...arvotut, luku];
            arvotut.sort((a, b) => a - b);
          } else {
            kpl--;
          }
        }
      }
      rivienLkm = 0;
    }
    document.getElementById('hide').style.display = 'none';
  }
</script>

<main>
  <Info tekija={arpoja} />

  <h2>Maagisia rivejä tulossa ({rivienLkm}/1)</h2>

  <button id="hide" on:click={lisaaRivi}>Lisää rivi</button>

  <button on:click={nollaa}>Nollaa</button>

  <button on:click={lottoKone}>Aloita arvonta</button>

  <div id="boxi">
    {#each arvotut as arvottu}
      <p in:fly={{ duration: 1500, x: 300, y: 300 }} out:fade id="arvottuja">
        {arvottu}
      </p>
    {/each}
  </div>

  {#if rivienLkm === 0}
    <p>Pistetäänkö riviä tulemaan?</p>
  {:else}
    <p>Klikkaa vielä "Aloita arvonta!"</p>
  {/if}
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
    background-color: rgb(255, 217, 4);
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }

  #arvottuja {
    background-color: #ff3e00;
    border: 2px solid black;
    width: 100px;
    margin: 10px;
  }

  #boxi {
    display: flex;
    flex-direction: row;
    justify-content: center;
    flex-wrap: wrap;
  }
</style>
