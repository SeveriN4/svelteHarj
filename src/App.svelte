<script>
  //importattuna lottorivin tulostamiseen käytetyt animaatiot
  //ja Info ja Rivinimi komponentit
  import { fly, fade } from 'svelte/transition';
  import Info from './Info.svelte';
  import Rivinimi from './Rivinimi.svelte';

  //propseihin liittyviä muuttujia
  let arvo = false;
  let nimi = '';
  let arpoja = 'Severi';

  //validointia
  const onkoValidiNimi = (x) => x.length > 0;
  $: validiNimi = onkoValidiNimi(nimi);

  //lottokoneen toimintaan liittyviä muuttujia
  let rivienLkm = 0;
  let maxNro = 40;
  let minNro = 1;
  let arvotut = [];

  //funktioita joilla lisätään arvottava rivi ja nollaa funktio joka alottaa
  //lottokoneen alusta
  function lisaaRivi() {
    rivienLkm++;
  }

  function nollaa() {
    rivienLkm = 0;
    arvotut = [];
    //alempi rivi tutoriaalista
    document.getElementById('hide').style.display = '';
    arvo = false;
    nimi = '';
  }

  //itse lottokone
  function lottoKone() {
    if (rivienLkm > 1 || rivienLkm === 0) {
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
          //tästä 3 riviä alaspäin otettu mallia tutoriaalista
          if (luku !== arvotut[luku]) {
            arvotut = [...arvotut, luku];
            arvotut.sort((a, b) => a - b);
          } else {
            kpl--;
          }
        }
      }
      rivienLkm = 0;
      //alempi rivi tutoriaalista
      document.getElementById('hide').style.display = 'none';
      arvo = true;
    }
  }
</script>

<main>
  <!-- Info komponentti joka tuo oikestaan vaan headerin johon on völitetty propsina tekijän nimi-->
  <Info tekija={arpoja} />

  <h2>Maagisia rivejä tulossa ({rivienLkm}/1)</h2>

  <!-- Pari on click tapahtumaa liittyen lottokoneen toimintaan-->
  <button id="hide" on:click={lisaaRivi}>Lisää rivi</button>

  <button on:click={nollaa}>Nollaa</button>

  <button on:click={lottoKone}>Aloita arvonta</button>

  <h2 id="nametag">{nimi}</h2>

  <!-- each lohko johon lottorivin 7 numeroa tulostetaan animaatioiden kera, myös poistuminen nollaa funktiolla animoitu-->
  <div id="boxi">
    {#each arvotut as arvottu}
      <p in:fly={{ duration: 1500, x: 300, y: 300 }} out:fade id="arvottuja">
        {arvottu}
      </p>
    {/each}
  </div>

  <!-- rivinimi komponentti johon tehty pari propsien sidontaa-->
  <Rivinimi bind:onkoArvottu={arvo} bind:name={nimi} isValid={validiNimi} />
</main>

<style>
  /* css tästä eteenpäin */
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

  #nametag {
    font-style: italic;
    color: #ff3e00;
  }
</style>
