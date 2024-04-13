<script>
  import * as d3 from "d3"
  import {onMount} from "svelte"

  /* Array donde guardaremos la data */
  let datos_morfi = []

  /* 1. Escala par lugar de comida */
  /*let colorLugar = d3.scaleOrdinal()
    .domain(["Mingo", "Fud", "Green Bites", "El Rincón", "Havana", "Traigo de casa"])
    .range(["#ff8c8c", "#ff814a", "#458330", "#71372a", "#ffc700", "#ff2f48"])

  /* 2. Escala para mejor café */
  /*let colorCafe = d3.scaleOrdinal
    .domain(["Havana", "Fud"])
    .range(["#ffb700", "#71372a"])

  /* 3. Escala para gaston en comida */
  let gasto = d3.scaleLinear().range([0, 200])

  /* Creo que nada más necesita escala */

  onMount(() => {
    d3.csv("./data/MorfiFacu-sheet.csv", d3.autoType).then(data => {
      console.log(data)

      let MinMaxGasto = d3.extent(data, d => d.gastoPromedio)
      gasto =gasto.domain(MinMaxGasto)

      datos_morfi = data
    })
  })

</script>

<main>
  <div class="header">
    <h3 class="headline">
      Morfi en la facu
    </h3>
    <p class="bajada">Lugares más elegidos, habitos y puntuación del tostado de Mingo &#129386</p>
  </div>

  
  <!-- Conedor de las entidades -->
  <!--<div class="container"> -->
    <!-- Iteramos la data para visualizar c/ entidad -->
    <!--{#each deportistas as dep}
      <div class="person-container">
        <div class="medal"
          style="background-color: {colorMedalla(dep.medalla)}"
          ></div>
        <div
          class="person"
          style="border-width: {grosor(dep.edad)}px; 
        background-color:{colorGenero(dep.genero)}; 
        width: {2 * radioAltura(dep.altura)}px; 
        height: {2 * radioAltura(dep.altura)}px; 
        border-color: {colorContinentes(dep.continente)}"
        ></div>
        <p class="name">
          <b>{dep.nombre}</b>
          <br />
          {dep.continente}
        </p>
      </div>
    {/each}
  </div> -->
</main>

<style>
  .header {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    margin-top: 50px;
    margin-bottom: 80px;
  }
  .headline {
    font-size: 40px;
    line-height: 1;
    font-weight: bold;
    text-align: center;
    margin: 20px;
  }
  .bajada {
    font-size: 18px;
    font-weight: normal;
    text-align: center;
    margin: 10px;
  }
  /*.headline b {
    display: block;
  }
  .container {
    display: flex;
    justify-content: center;
    align-items: end;
    margin: auto;
    flex-wrap: wrap;
    max-width: 1000px;
    gap: 30px;
    margin-bottom: 100px;
  }
  .person-container {
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
    flex: 180px 0 0;
  }
  .person {
    width: 100px;
    height: 100px;
    border: 10px solid black;
    border-radius: 50%;
    box-sizing: border-box;
    background-color: pink;
  }
  .medal {
    width: 15px;
    height: 15px;
    border-radius: 50%;
    background-color: gold;
    margin: 5px 0;
  }
  .name {
    font-size: 14px;
    color: rgb(65, 65, 65);
    font-weight: normal;
    text-align: center;
    margin-top: 5px;
  }*/
</style>
