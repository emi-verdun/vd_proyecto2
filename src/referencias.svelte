<script>
  import * as d3 from "d3"
  import {onMount} from "svelte"

    
  let colores1 = ["#458330"]
  let colores2 = ["#ff8c8c","#7A1F3D"]
  let colores3 = ["#71372a", "#ffc700", "#ff2f48"]
  let opciones = [colores1, colores2, colores3]

  let puntuacion = ["Tostado: 1 estrella", "Tostado: 3 estrellas", "Tostado: 5 estrellas"]
  let plato1 = [30, 72, 120]
  let plato2 = [15, 48, 80]

  onMount(() => {
    d3.csv("./data/referencias.csv", d3.autoType).then(data => {
      console.log(data)
    })
  })
</script>

<main>
  <!-- Contenedor de las entidades -->
  <div class="cont-grande">
    <div class="pizarra">

      <div class="corcheteContainer">
        <div class="corchetes">
          <img src="./images/corchete.svg" alt="corchete" style="height:30px">
          <img src="./images/corchete.svg" alt="corchete" style="height:50px">
          <img src="./images/corchete3.svg" alt="corchete" style="height:70px">
        </div>
      </div>

      <div class="frecuenciaContainer">
        <div class="frecuencia">
          <p id="d_1">1 día</p>
          <p id="d_2">2 días</p>
          <p id="d_3">3 días</p>
        </div>
      </div>

      <div class="tostadoContainer">
        <div class="parrafos_punt">
          {#each [0,1,2] as i}
          <p>{puntuacion[i]}</p>
          {/each}
        </div>
        <div class="lineas_long">
          <img src="./images/corchete.svg" alt="long" style="height: 30px; transform:rotate(-90deg)">
          <img src="./images/corchete.svg" alt="long" style="height: 80px;transform:rotate(-90deg)">
          <img src="./images/corchete.svg" alt="long" style="height: 120px;transform:rotate(-90deg)">
        </div>
      </div>

      <div class="flechas">
        <img id="f_f" style="height: 10px" src="./images/flecha.svg" alt="flechita">
        <img id="f_m" style="height: 10px" src="./images/flecha.svg" alt="flechita">
        <img id="f_g" style="height: 10px" src="./images/flecha.svg" alt="flechita">
        <img id="f_r" style="height: 10px" src="./images/flecha.svg" alt="flechita">
        <img id="f_h" style="height: 10px" src="./images/flecha.svg" alt="flechita">
        <img id="f_c" style="height: 10px" src="./images/flecha.svg" alt="flechita">
      </div>
      
      <div class="lugares">
        <p id="p_f">Fud</p>
        <p id="p_m">Mingo</p>
        <p id="p_g">Green Bites</p>
        <p id="p_r">El Rincon</p>
        <p id="p_h">Havanna</p>
        <p id="p_c">Casa</p>
      </div>

      <div class="container">

        <h3>Menú</h3>

        <div class="sang_pla">
          <div class="sanguches_ref">
              {#each opciones as colores}
                  <div class="no_plato">  
                  {#each colores as n}
                      <div class="pan">
                      <div class="relleno">
                          <div class="fill_1"
                          style="background-color: {n};
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
                  {/each}
                  </div>
              {/each}
          </div>

          <div class="platillos">
              {#each [0,1,2] as i}
              <div class="plato"
                  style ="display:flex;
                  flex-direction: column;
                  align-items: center; width:120px">
                  <div 
                      style= "background-color: #bfc0c0;
                      width: {plato1[i]}px;
                      height: 7px"
                  ></div>
                  <div 
                      style = "background-color: #bfc0c0;
                      width: {plato2[i]}px;
                      height: 7px"
                  ></div> 
              </div>
              {/each}
          </div>
      
        </div>

        <div class="cafeContainer">
          <div class="preferencia_cafe">
            <p>Café Fud</p>
            <p>Café Havanna</p>
          </div>
          <div class="cafe">
              <div>
                <div class = "cafe-wrapper">
                    <div class = "cafe-column" style="height:20%;"></div>
                    <img id ="img_f" style = "height: 50px" src="./images/cafe_fud2.svg" alt="Café de Fud">
                </div>
                <img class="fc" style="height: 20px" src="./images/flecha.svg" alt="flechita">
                <p id="p1">$1500</p>
                </div>
                <div>
                <div class = "cafe-wrapper">
                    <div class = "cafe-column" style="height:90%;"></div>
                    <img id ="img_h" style = "height: 50px" src="./images/cafe_havana2.svg" alt="Café de Hacanna">
                </div>
                <img class="fc" style="height: 20px" src="./images/flecha.svg" alt="flechita">
                <p id="p2">$6000</p>
              </div>
          </div>
        </div>
        
        

        <div class="serv">
          <p style="font-size:23px; margin-bottom:25px">Calidad del servicio</p>
          <div class="servicio">
            <p style="font-size:20px">0</p>
            <img style= "height: 30px" src="/images/servicio1.svg" alt="Rating de Servicio = 0-1">
            <img style= "height: 16px" src="/images/servicio2.svg" alt="Rating de Servicio = 0-1">
            <div style="height:40px; width:40px"></div>
            <img style= "height: 30px" src="/images/servicio4.svg" alt="Rating de Servicio = 0-1">
            <img style= "height: 40px" src="/images/servicio5.svg" alt="Rating de Servicio = 0-1">
            <p style="font-size:20px">5</p>
          </div>
        </div>
        
  
        <div class="cont-ref">
            <p class="referencias" id="titulo-ref">Referencias</p>
            <p class="referencias"> <br><br><br><br><br><br><br><br><br><br><br><br><br> <u>Cantidad de Sandwiches</u>:  Días que se come en la facultad</p>
            <p class="referencias"> <br><br><br><br><br> <u>Relleno de Sandwiches</u>:  Preferencia de comida de tal lugar</p>
            <p class="referencias"> <br><br><br><br><br> <u>Longitud del plato</u>:  Rating del tostado de Mingo</p>
            <p class="referencias"> <br><br><br><br><br> <u>Mosquinha o brillitos</u>:  Calidad del servicio del lugar elegido</p>
            <p class="referencias"> <br><br><br><br><br> <u>Color Vaso Café</u>:  Preferencia de café de tal lugar</p>
            <p class="referencias"> <br><br><br><br><br> <u>Relleno vaso</u>:  Gasto promedio en comida</p>
        </div> 

      </div>
    </div>
  </div>
</main>

<style>
  .cont-grande{
    display:flex;
    justify-content: center;
}
  .pizarra{
    display: flex;
    justify-content: center;
    width: 1000px;
    height: 1100px;
    background-color: rgba(35, 107, 36, 0.8);
    border:solid 5px rgba(143, 95, 12, 0.8);
    position: relative;
  }
  .container{
    display: flex;
    flex-direction: column;
    justify-content: center;
    flex-wrap: wrap;
    width: 70%;
    height: 1000px;
  }


  h3{
   font-family: Homemade Apple; 
   font-size: 40px; 
   color: white; 
   width: 100%;
   text-align: center;
  }


  .sang_pla{
    position: relative;
    margin-bottom: 130px;
  }
  .sanguches_ref{
    display: flex;
    align-items: end;
    justify-content: center;
    position:relative;
    column-gap: 240px;
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
  .platillos{
    display: flex;
    align-items: end;
    position:relative;
    justify-content: center;
    column-gap: 182px;
  }

  .corcheteContainer{
    position: absolute;
    top: 15.5%;
    left: 17%;
  }
  .corchetes{
    display: flex;
    align-items: end;
    column-gap: 290px;
    position: relative;
  }
  .frecuenciaContainer{
    position: absolute;
    top: 17%;
    left: 13%;
  }
  .frecuencia{
    display:flex;
    column-gap: 250px;
    position:relative;
  }
  .tostadoContainer{
    position: absolute;
    width: 100%;
    margin-top: 2px;
    top: 22%;
    left: 8.5%;
  }
  .parrafos_punt{
    display:flex;
    margin-top: 20px;
    column-gap: 160px;
    left: 60px;
    position:relative;
  }
  .lineas_long{
    display:flex;
    flex-direction: row;
    align-items: center;
    column-gap: 290px;
    position: absolute;
    bottom: 5px;
    left: 125px;
  }
  .flechas{
    position: absolute;
    width: 100%;
    height: 100%;
    top:24%;
    left: 9%;
  }
  .lugares{
    position: absolute;
  }
  #f_f{position:relative; left:152px; bottom: 45px}
  #f_m{position:relative; left:715px; bottom:65px;}
  #f_g{position:relative; left:373px; bottom:45px}
  #f_r{position:relative; left:635px; bottom:85px}
  #f_h{position:relative; left:292px; bottom:65px;}
  #f_c{position:relative; left:555px; bottom:45px;}
  
  #p_f{position:relative; top:195px; right:200px;}
  #p_m{position:relative; top:120px; left:112px}
  #p_g{position:relative; top:100px; left:130px}
  #p_r{position:relative; top:0px;left:425px}
  #p_h{position:relative; bottom:25px;left:420px}
  #p_c{position:relative; bottom:50px; left:405px}


  .cafeContainer{
    width: 100%;
    display: flex;
    justify-content: center;
    position: relative;
  }
  .cafe{
    display:flex;
    position: relative;
    column-gap: 200px;
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
    left: 15%;
    right: 10%;
    bottom: 5%;
    background-color: #2F1D12;
    z-index: 1;
  }
  #img_h, #img_f {
    position:absolute;
    z-index: 20;
  }
  .fc{
    position:relative;
    left:20px;
    bottom:18px;   
    z-index: 10;
  }
  #p1,#p2{
    position:relative;
    bottom:75px;
    left:83px;
    font-size:22px;
  }
  .preferencia_cafe{
    display:flex;
    column-gap: 180px;
    position:absolute;
    bottom: 40px;
    width: 100%;
    justify-content: center;
    margin-right: 20px;
  }
  

  .serv{
  display: flex;
  flex-direction: column;
  justify-content: center;
  position: relative;
  margin-bottom: 40px;
  margin-top: -10px;
 }
  .servicio{
    display:flex;
    flex-direction: row;
    justify-content: center;
    column-gap: 60px;
    position:relative;
  }


  .cont-ref{
    position:relative;
    width: 100%;
    margin-top: 40px;
  }
  .referencias{
    text-align: start;
    line-height: .8px;
  }
  #titulo-ref{
    font-size:22px;
  }


  p{
    font-family: Satisfy;
    font-size: 20px;
    color:white;
    text-align: center;
  }

</style>