<script setup>
const slike = {
    "Jabuka": "https://www.svgrepo.com/show/530203/apple.svg",
    "Mrkva": "https://www.svgrepo.com/show/530216/carrot.svg",
    "Sir": "https://www.svgrepo.com/show/530219/cake.svg",
    "Kruh": "https://www.svgrepo.com/show/530223/bread.svg",
}
const proizvodi = [
    { naziv: "Jabuka", cijena: 0.25 },
    { naziv: "Mrkva", cijena: 0.12 },
    { naziv: "Kruh", cijena: 2.00 },
    { naziv: "Sir", cijena: 4.48 }
]
const korisnik = {
    jeAdmin: true,
    osobni_podaci: {
    ime: "Marko",
    prezime: "Krivić",
    adresa: {
    grad: "Pula",
    ulica: "Veruda",
    broj: 32
    },
    broj_telefona: "+091-123-456"
    },
    kosarica: [
    { naziv: "Jabuka", količina: 4 },
    { naziv: "Mrkva", količina: 12 },
    { naziv: "Sir", količina: 1 },
    { naziv: "Kruh", količina: 3 },
    ]
}
const kosara = "https://www.harissa.hr/images/prazna-kosarica.svg"
function dohvatiCijenu(naziv) {
  for (let i in proizvodi) {
    if (naziv == proizvodi[i].naziv) {
      return proizvodi[i].cijena
    }
  }
}
function sveukupnaCijena() {
  return korisnik.kosarica.reduce((sum, stavka) => {
    let proizvod = proizvodi.find(p => p.naziv === stavka.naziv);
    return proizvod ? sum + stavka.količina * proizvod.cijena : sum;
  }, 0).toFixed(2);
}
function najskupljaStavka() {
      let maxStavka = "";
      let maxCijena = 0;
      
      korisnik.kosarica.forEach(stavka => {
        let proizvod = proizvodi.find(p => p.naziv === stavka.naziv);
        if (proizvod) {
          let ukupnaCijena = stavka.količina * proizvod.cijena;
          if (ukupnaCijena > maxCijena) {
            maxCijena = ukupnaCijena;
            maxStavka = stavka.naziv;
          }
        }
      });
      return maxStavka;
}
</script>

<template>
    <div class="bg-pink-200 p-3 m-1 text-[15px] text-pink-600 rounded-sm">
        <div :class="korisnik.jeAdmin ? 'text-blue-800' : 'text-black' ">
          <p class="pb-1 font-bold">Korisnički podaci</p> <hr class="opacity-50">
          <p><b>Ime:</b> {{ korisnik.osobni_podaci.ime}} {{ korisnik.osobni_podaci.prezime }}</p> 
          <p><b>Adresa:</b> {{korisnik.osobni_podaci.adresa.grad}} {{korisnik.osobni_podaci.adresa.ulica}} {{korisnik.osobni_podaci.adresa.broj}}</p>
          <p><b>Telefon:</b> {{ korisnik.osobni_podaci.broj_telefona }}</p>
        </div>  
    </div>

    <div class="bg-pink-200 m-1 p-3 rounded-sm"> 
      <div class="flex items-center ">
        <img :src="kosara" alt="kosara" class="w-15 h-15  p-1">
        <p class="p-1 text-2xl">Košarica</p> 
      </div>
      <div class="border-1 rounded-[10px] border-pink-400 flex p-1 mb-2 bg-pink-300" :class="{'bg-red-300 border-red-500': proizvodi[0].naziv==najskupljaStavka()}">
          <img :src="slike.Jabuka" alt="jabuka" class="w-17 h-17 p-3"> 
          <div>
              <b> {{ proizvodi[0].naziv }}</b>
              <p>Cijena: €{{ dohvatiCijenu("Jabuka") }} | Količina: {{korisnik.kosarica[0].količina  }}</p>
              <p>Ukupno: €{{ (proizvodi[0].cijena*korisnik.kosarica[0].količina).toFixed(2) }} </p>
          </div>
        </div>

        <div class="border-1 rounded-[10px] border-pink-400 flex p-1 mb-2 bg-pink-300" :class="{'bg-red-300 border-red-500': proizvodi[1].naziv==najskupljaStavka() }">
            <img :src="slike.Mrkva" alt="mrkva" class="w-17 h-17 p-3"> 
            <div>
              <b> {{ proizvodi[1].naziv }}</b>
              <p>Cijena: €{{ dohvatiCijenu("Mrkva") }} | Količina: {{korisnik.kosarica[1].količina  }}</p>
              <p>Ukupno: €{{ (proizvodi[1].cijena*korisnik.kosarica[1].količina).toFixed(2) }} </p>
            </div>
        </div>

        <div class="border-1 rounded-[10px] border-pink-400 flex p-1 mb-2 bg-pink-300" :class="{'bg-red-300 border-red-500': proizvodi[2].naziv==najskupljaStavka()}">
            <img :src="slike.Kruh" alt="kruh" class="w-17 h-17 p-3"> 
            <div>
              <b> {{ proizvodi[2].naziv }}</b>
              <p>Cijena: €{{ dohvatiCijenu("Kruh") }} | Količina: {{korisnik.kosarica[3].količina  }}</p>
              <p>Ukupno: €{{ (proizvodi[2].cijena*korisnik.kosarica[3].količina).toFixed(2) }} </p>
            </div>
        </div>

        <div class="border-1 rounded-[10px] border-pink-400 flex p-1 mb-2 bg-pink-300" :class="{'bg-red-300 border-red-500': proizvodi[3].naziv==najskupljaStavka()}">
            <img :src="slike.Sir" alt="sir" class="w-17 h-17 p-3"> 
            <div>
              <b> {{ proizvodi[3].naziv }}</b>
              <p>Cijena: €{{ dohvatiCijenu("Sir") }} | Količina: {{korisnik.kosarica[2].količina  }}</p>
              <p>Ukupno: €{{ (proizvodi[3].cijena*korisnik.kosarica[2].količina).toFixed(2) }} </p>
            </div>
          </div>
          <p class="pt-2 pb-2"><b>Ukupna cijena: </b> €{{sveukupnaCijena() }}</p>
    </div>
</template>

<style scoped>

</style>
