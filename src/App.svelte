<script>
  import * as d3 from "d3"
  import {onMount} from "svelte"
  import Referencias from "./referencias.svelte"

  
  /* Array donde guardaremos la data */
  let datos_morfi = []


  /* 1. Escala par lugar de comida */
  let colorLugar = d3.scaleOrdinal()
    .domain(["Mingo", "Fud", "Green Bites", "El Rincon", "Havana", "Traigo de casa"])
    .range(["#ff8c8c", "#458330", "#ff814a", "#71372a", "#ffc700", "#ff2f48"])

  /* 2. Escala para gaston en comida */
  let gasto = d3.scaleLinear([0, 6500],[0, 100])

  /* 3. Escala para cantidad de días que come en la facultad */
  let cantDias = d3.scaleOrdinal()
    .domain([0,1,2,3,4,5])
    .range([1,1,2,3,4,5])

  /* 4. Escala para rating de servicio */
  let servicio = d3.scaleOrdinal()
    .domain([0,1,2,3,4,5])
    .range([1,1,2,3,4,5])
  
    let gap = (5-1)/6
  
  /* 5. Escala para rating del tostado de Mingo */
  let tostadoM1 = d3.scaleBand()
    .domain([0,1,2,3,4,5])
    .range([30, 120])
  
  let tostadoM2 = d3.scaleBand()
  .domain([0,1,2,3,4,5])
  .range([15, 80])

  onMount(() => {
    d3.csv("./data/MorfiFacu-sheet.csv", d3.autoType).then(data => {
      console.log(data)

      datos_morfi = data
    })
  })

</script>


<main>
  <div class="header">
    <div class="header2">
      <h3 class="headline">
        Morfi en la Facu
      </h3>
      <p class="bajada">Lugares más elegidos, habitos y puntuación del tostado de Mingo &#129386</p>
    </div>
    <div class="skewed"></div>
  </div>

  <!-- Contenedor de las entidades -->
  <div class="container">

    {#each datos_morfi as sangu}
      <div class="todo">
        <!-- Contenedor comida de cada persona -->
        <div class="comida-container">
          <div class="mantel"></div>
          <div class="sanguches">
            <div class="no_plato">  
            {#each d3.range(1, 6) as n}
                {#if n <= [cantDias(sangu.cantDias)]}

                <div class="pan">
                  <div class="relleno">
                    <div class="fill_1"
                      style="background-color: {colorLugar(sangu.lugar)};
                      height: 3.5px;
                      width: 60px;" 
                    ></div>
                    <div class="fill_2"
                      style="background-color: yellow;
                      height: 3.5px;
                      width: 60px;" 
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
                style= "background-color: #bfc0c0;
                width: {tostadoM1(sangu.tostadoMingo)}px;
                height: 7px"
              ></div>
              <div 
                style = "background-color: #bfc0c0;
                width: {tostadoM2(sangu.tostadoMingo)}px;
                height: 7px"
              ></div> 
            </div>
          </div>
          
          <div class="cafe">
            <div>
              <div class = "cafe-wrapper">
                <div class = "cafe-column" style="height:{gasto(sangu.gastoPromedio)}%;"></div>
                {#if sangu.mejorCafe == 'Havana'}  
                  <img id="img_h" style= "height: 50px" src="./images/cafe_havana2.svg" alt="Café de Havanna">
                {:else}
                  <img id ="img_f" style = "height: 50px" src="./images/cafe_fud2.svg" alt="Café de Fud">
                {/if}
              </div>
            </div>
          </div>

          <div class="servicio" style="margin-bottom: {60+(cantDias(sangu.cantDias)*gap)*20}px">
            {#if 1 == [servicio(sangu.ratingServicio)]}
              <img style= "height: 30px" src="/images/servicio1.svg" alt="Rating de Servicio = 0-1">
            {:else if 2 == [servicio(sangu.ratingServicio)]}
              <img style= "height: 16px" src="/images/servicio2.svg" alt="Rating de Servicio = 2">
            {:else if 4 == [servicio(sangu.ratingServicio)]}
              <img style= "height: 30px" src="/images/servicio4.svg" alt="Rating de Servicio = 4">
            {:else if 5 == [servicio(sangu.ratingServicio)]}
              <img style= "height: 40px" src="/images/servicio5.svg" alt="Rating de Servicio = 5">
            {/if}
          </div>
        </div>
        <div class="nombre"> <p class="nom_text"> {sangu.nombre} </p> </div>
      </div>
    {/each}

  </div>


  <!--ARMAMOS MENU DE REFERENCIAS-->
  <div class="referencias_menu">
    <Referencias />

  </div>

</main>

<footer class="footer">
  <div class="text_ft">
    <p class="text"> by Maru y Emi</p>
  </div>
  <div class="contenido">
    <div class="links">
      <a href="https://github.com/emi-verdun/vd_proyecto2" target="_blank"><img src="/images/github.svg" alt="logo github" style="width: 45px; height:45px; margin-right:15px"></a>
      <a href="https://www.figma.com/design/PJKDFxw6OxdUhHQPw3vxXf/Presentacion-VD?node-id=0%3A1&t=VZAbxec0ld5lxipf-1" target="_blank"><img src="/images/figma.svg" alt="logo figma" style="width: 45px; height:45px"></a>
    </div>
    <div><p id="link"> LINKS DEL PROYECTO </p></div>
  </div>
</footer>


<style>

.skewed {
  z-index:2;
  position: absolute;
  top: 0;
  bottom: 0;
  right: 0;
  left: 0;
  width: 100%;
  height: 280px;
  z-index: 0;
  background: linear-gradient(0deg, rgba(255, 0, 0, 0.389) 15px, transparent 15px), linear-gradient(90deg, rgba(255, 0, 0, 0.5) 15px, transparent 15px), #FFF;
  background-size: 35px 35px;
  }
  
  .header2 {
    background-color:#4a4a4a; 
    z-index:3;
    width: 700px;
  }

  .header {
    z-index: 1;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    margin-top: 50px;
    margin-bottom: 120px;
  }

  .headline {
    z-index: 4; 
    font-size: 50px;
    color: white;
    font-family: Ojuju;
    line-height: 1;
    font-weight: 700;
    text-align: center;
    margin: 20px;
  }

  .bajada {
    z-index: 4;
    color: white;
    font-size: 18px;
    font-family: sans-serif;
    font-weight: bold 700;
    text-align: center;
    margin: 5px;
    margin-bottom: 20px;
  }

  .container {
    display: flex;
    flex-direction: row;
    align-items: flex-end;
    flex-wrap: wrap;
    column-gap: 120px;
    row-gap: 60px;
    margin-bottom: 150px;
    margin-right: 210px;
    margin-left: 210px;
  }

  .nombre {
    display: none;
    background-color: rgba(243, 243, 243, 0.6);
    z-index: 3;
    margin-bottom: -50px;
    width: max-content;
  }

  .nom_text {
    text-align: center;
    font-size: 20px;
    font-weight: 500;
    font-family: sans-serif;
    margin: auto;
    padding-left: 5px;
    padding-right: 5px;
  }

  .todo {
    border-color: #FFF;
    position: relative;
    display: flex;
    justify-content: center;
    align-items: flex-end; /*saco = nombres arriba*/
    flex: 180px 0 0;
    height: 150px;
    z-index: 1;
  }

  .comida-container {
    position: relative;
    display: flex;
    justify-content: center;
    align-items: flex-end;
    flex: 180px 0 0;
    height: 150px;
    z-index: 1;
  }

  .comida-container:hover + .nombre {
    display: grid;
    position: absolute;
	  align-items: center;
    z-index: 5;
  }

  .mantel {
    position: absolute;
    height: 20px;
    width: 180px;
    margin-bottom: -10px;
    background: repeating-linear-gradient(45deg, transparent, transparent 5%, rgba(255, 0, 0, 0.389) 5%,
    rgba(255, 0, 0, 0.389) 10%, transparent 10%, transparent 15%, rgba(255, 0, 0, 0.5) 15%, rgba(255, 0, 0, 0.5) 20%),
    repeating-linear-gradient(-45deg, transparent, transparent 5%, rgba(255, 0, 0, 0.389) 5%,
    rgba(255, 0, 0, 0.389) 10%, transparent 10%, transparent 15%, rgba(255, 0, 0, 0.5) 15%, rgba(255, 0, 0, 0.5) 20%);  
    background-color:#FFF;
    z-index: 1;
  }


  .sanguches{
    display:flex;
    flex-direction: column;
    align-items: center;
    position: absolute;
    margin-left: 50px;
    z-index: 2;
  }

  .pan {
    background-color: #f3efc7;
    width: 60px;
    height: 20px;
    display: flex;
    justify-content:center;
    align-items: center;
    border-style: solid;
    border-width: 1px;
    border-color: #f7c871
  }
  
  .servicio{
    position: absolute;
    margin-left: 90px;
    z-index: 2;
   }

   .cafe{
    display:flex;
    position: absolute;
    margin-right: 120px;
    margin-bottom: -6px;
    z-index: 2;
  }

   .cafe-wrapper {
    position: relative;
    width: 42.5px;
    height: 50px;
    z-index: 1;
  }
  .cafe-column{
    position: absolute;
    height: 50%;
    left: 14%;
    right: 10%;
    bottom: 5%;
    background-color: #2F1D12;
    z-index: 1;
  }

  #img_h, #img_f {
    position:absolute;
    z-index: 20;
  }

  .footer{
  display: flex;
  flex-direction: row;
  column-gap: 1000px;
  justify-content: center;
  align-items: center;
  width: 100%;
  margin-top: 100px;
  margin-bottom: -10px;
  margin-left: -10px;
  padding-right: 18px;
  height: 100px;
  background-color:rgba(32, 32, 32, 0.8);
}
.text_ft{
  display: flex;
  align-items: center;
  margin-left: 40px;
  height: 60px;
  padding-left: 10px;
  padding-right: 10px;
}
.text{
  color: rgba(255, 255, 255, 0.6);
  font-size: 18px;
  font-family: sans-serif;
  font-weight: bold 700;
  text-align: center;
}
#link{
  font-size: 15px;
  font-family: sans-serif;
  font-weight: 700;
  color: white;
}
.contenido{
  display: flex;
  flex-direction: row;
  column-gap: 30px;
}

</style>
