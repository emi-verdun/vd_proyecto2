<script>
  import * as d3 from "d3"
  import {onMount} from "svelte"

  
  /* Array donde guardaremos la data */
  let datos_morfi = []


  /* 1. Escala par lugar de comida */
  let colorLugar = d3.scaleOrdinal()
    .domain(["Mingo", "Fud", "Green Bites", "El Rincon", "Havana", "Traigo de casa"])
    .range(["#ff8c8c", "#ff814a", "#458330", "#71372a", "#ffc700", "#ff2f48"])

  /* 2. Escala para mejor café */ /*NO SE USA, NO DEJA USARLO CON SVG EN ESTE ARCHIVO, BORRA LA PAGINA*/
  /*let colorCafe = d3.scaleOrdinal
    .domain(["Havana", "Fud"])
    .range(["#ffb700", "#71372a"])

  /* 3. Escala para gaston en comida */
  let gasto = d3.scaleLinear().range([0, 200])

  /* 4. Escala para cantidad de días que come en la facultad */
  let cantDias = d3.scaleOrdinal()
    .domain([0,1,2,3,4,5])
    .range([1,1,2,3,4,5])

  /* 5. Escala para rating de servicio */
  let servicio = d3.scaleOrdinal()
    .domain([0,1,2,3,4,5])
    .range([1,1,2,3,4,5])
  
  /* 6. Escala para rating del tostado de Mingo */
  let tostadoM1 = d3.scaleBand()
    .domain([0,1,2,3,4,5])
    .range([30, 80])
  
  let tostadoM2 = d3.scaleBand()
  .domain([0,1,2,3,4,5])
  .range([10, 60])


  onMount(() => {
    d3.csv("./data/MorfiFacu-sheet.csv", d3.autoType).then(data => {
      console.log(data)

      let MinMaxGasto = d3.extent(data, d => d.gastoPromedio)
      gasto = gasto.domain(MinMaxGasto)

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
  <div class="container">

    {#each datos_morfi as sangu}

      <!-- Contenedor comida de cada persona -->
      <div class="comida-container">

        <div class="sanguches">
          {#each d3.range(1, 6) as n}
            {#if n <= [cantDias(sangu.cantDias)]}

              <div class="pan">
                <div class="relleno">
                  <div class="fill_1"
                    style="background-color: {colorLugar(sangu.lugar)};
                    height: 3px;
                    width: 50px;" 
                  ></div>
                  <div class="fill_2"
                    style="background-color: yellow;
                    height: 3px;
                    width: 50px;" 
                  ></div>
                </div>
              </div>

            {/if} 
          {/each}
        </div>

        <div class="plato"
          style ="display:flex;
          flex-direction: column;
          align-items: center">
          <div 
            style= "background-color: grey;
            width: 80px;
            height: 5px"
          ></div>
          <div 
            style = "background-color: grey;
            width: 60px;
            height: 5px"
          ></div> 
        </div>

        <div class="cafe">
          {#if sangu.mejorCafe == 'Havana'}
            <img style= "height: 45px" src="/images/cafeHavanna.svg" alt="Café de Havanna">
          {:else}
            <img style= "height: 45px" src="/images/cafeFud.svg" alt="Café de Fud">
          {/if}
        </div>

        <div class="servicio">
          {#if 1 == [servicio(sangu.ratingServicio)]}
            <img style= "height: 30px" src="/images/servicio1.svg" alt="Rating de Servicio = 0-1">
          {:else if 2 == [servicio(sangu.ratingServicio)]}
            <img style= "height: 12px" src="/images/servicio2.svg" alt="Rating de Servicio = 2">
          {:else if 4 == [servicio(sangu.ratingServicio)]}
            <img style= "height: 25px" src="/images/servicio4.svg" alt="Rating de Servicio = 4">
          {:else if 5 == [servicio(sangu.ratingServicio)]}
            <img style= "height: 35px" src="/images/servicio5.svg" alt="Rating de Servicio = 5">
          {/if}
        </div>

      </div>

    {/each}

  </div> 
</main>


<style>

  .header {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    margin-top: 50px;
    margin-bottom: 80px;
    background-color: whitesmoke;
  }

  .headline {
    font-size: 40px;
    font-family: Passion One;
    text-transform: uppercase;
    word-spacing: 1px;
    line-height: 1;
    font-weight: normal;
    text-align: center;
    margin: 20px;
  }

  .bajada {
    font-size: 18px;
    font-family: sans-serif;
    font-weight: normal;
    text-align: center;
    margin: 5px;
    margin-bottom: 20px;
  }

  .container {
    display: flex;
    justify-content: center;
    align-items: end;
    margin: auto;
    flex-wrap: wrap;
    gap: 40px;
    margin-bottom: 100px;
  }

  .comida-container {
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
    flex: 180px 0 0;
  }
  .pan {
    background-color: #fffbd6;
    width: 50px;
    height: 16px;
    display: flex;
    justify-content:center;
    align-items: center;
    border-style: solid;
    border-width: 1px;
    border-color: #ffe6b6
  }

</style>
