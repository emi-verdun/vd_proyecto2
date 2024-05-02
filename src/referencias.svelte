<script>
    import * as d3 from "d3"
    import {onMount} from "svelte"
  
    
    /* Array donde guardaremos la data */
    let datos_referencias = []
  
  
    /* 1. Escala par lugar de comida */
    let colorLugar = d3.scaleOrdinal()
      .domain(["Mingo", "Fud", "Green Bites", "El Rincon", "Havana", "Traigo de casa"])
      .range(["#ff8c8c", "#458330", "#7A1F3D", "#71372a", "#ffc700", "#ff2f48"])
  
    /* 2. Escala para gaston en comida */
    let gasto = d3.scaleLinear([0, 6000],[0, 100])
  
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
      d3.csv("./data/referencias.csv", d3.autoType).then(data => {
        console.log(data)
  
        datos_referencias = data
      })
    })
  
  </script>
  
  
  <main>
     <!-- Contenedor de las entidades -->
    <div class="container">
      <h3>Menú</h3>
  
      {#each datos_referencias as sangu}
  
        <!-- Contenedor comida de cada persona -->
        <div class="comida-container">
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
            <!-- {:else if 3 == [servicio(sangu.ratingServicio)]}
              <img style= "height: 16px" src="/images/servicio2.svg" alt="Rating de Servicio = 3"> -->
            {:else if 4 == [servicio(sangu.ratingServicio)]}
              <img style= "height: 30px" src="/images/servicio4.svg" alt="Rating de Servicio = 4">
            {:else if 5 == [servicio(sangu.ratingServicio)]}
              <img style= "height: 40px" src="/images/servicio5.svg" alt="Rating de Servicio = 5">
            {/if}
          </div>
        </div>
        <div class="texto-menu">
          <p><u>Cantidad</u>: {sangu.cantDias} día/s</p>
          <p><u>Relleno</u>: Morfi de {sangu.lugar}</p>
          <p><u>Vaso</u>: Café de {sangu.mejorCafe}</p>
          <p><u>Estado</u>:  Servicio de {sangu.ratingServicio} puntos</p>
          <p><u>Plato</u>: Tostado de Mingo es de {sangu.tostadoMingo} puntos</p>
          <p><u>Precio</u>: {sangu.gastoPromedio}$</p>
        </div>
      {/each}
  
    </div>
  </main>
  
  
  <style>
    .container {
      display: flex;
      flex-direction: column;
      align-items: start;
      margin: auto;
      flex-wrap: wrap;
      column-gap: 40px;
      row-gap: 40px;
      margin-left: 120px;
      width: 520px;
      background-color: green;
      border:solid 5px #9E772A;
    }
    h3{
     font-family: Homemade Apple; 
     font-size: 40px; 
     color: white; 
     margin-left: 200px;
    }
  
    .comida-container {
      position: relative;
      display: flex;
      justify-content: center;
      align-items: flex-end;
      height: 160px;
      margin-left: 90px;
      margin-bottom: 10px;
    }  
  
    .sanguches{
      display:flex;
      flex-direction: column;
      align-items: center;
      position: absolute;
      margin-left: 30px
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
      margin-left: 70px;
     }
  
     .cafe{
      display:flex;
      position: absolute;
      margin-right: 100px;
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
  
    .texto-menu {
      position: relative;
      margin-left: 170px;
      margin-top: -200px;
      line-height: 0.8;
    }
    p{
      font-family: Homemade Apple;
      font-size: 18px;
      color:white;
      text-align: center;
    }
  </style>
  