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
  <div class="container">
    <h3>Menú</h3>
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
    <div class="corchetes">
      <img src="./images/corchete.svg" alt="corchete" style="height:40px">
      <img src="./images/corchete.svg" alt="corchete" style="height:50px">
      <img src="./images/corchete3.svg" alt="corchete" style="height:70px">
    </div>
    <div class="frecuencia">
      <p id="d_1">1 día</p>
      <p id="d_2">2 días</p>
      <p id="d_3">3 días</p>
    </div>
    <div class="lineas_long">
      <img src="./images/corchete.svg" alt="long" style="height: 30px; transform:rotate(-90deg)">
      <img src="./images/corchete.svg" alt="long" style="height: 80px;transform:rotate(-90deg)">
      <img src="./images/corchete.svg" alt="long" style="height: 120px;transform:rotate(-90deg)">
    </div>
    <div class="parrafos_punt">
      {#each [0,1,2] as i}
        <p>{puntuacion[i]}</p>
      {/each}
    </div>
    
    <img id="f_f" style="height: 10px" src="./images/flecha.svg" alt="flechita">
    <img id="f_m" style="height: 10px" src="./images/flecha.svg" alt="flechita">
    <img id="f_g" style="height: 10px" src="./images/flecha.svg" alt="flechita">
    <img id="f_r" style="height: 10px" src="./images/flecha.svg" alt="flechita">
    <img id="f_h" style="height: 10px" src="./images/flecha.svg" alt="flechita">
    <img id="f_c" style="height: 10px" src="./images/flecha.svg" alt="flechita">
    <p id="p_f">Fud</p>
    <p id="p_m">Mingo</p>
    <p id="p_g">Green Bites</p>
    <p id="p_r">El Rincon</p>
    <p id="p_h">Havanna</p>
    <p id="p_c">Casa</p>
  </div>  

  <div class="preferencia_cafe">
    <p>Café Fud</p>
    <p>Café Havanna</p>
  </div>
  
  <div class="servicio">
    <p style="font-size:20px">0</p>
    <img style= "height: 30px" src="/images/servicio1.svg" alt="Rating de Servicio = 0-1">
    <img style= "height: 16px" src="/images/servicio2.svg" alt="Rating de Servicio = 0-1">
    <div style="height:40px; width:40px"></div>
    <img style= "height: 30px" src="/images/servicio4.svg" alt="Rating de Servicio = 0-1">
    <img style= "height: 40px" src="/images/servicio5.svg" alt="Rating de Servicio = 0-1">
    <p style="font-size:20px">5</p>
  </div>
  <p style="position:relative; bottom:710px; font-size:23px">Calidad del servicio</p>

  <div class="cont-ref">
    <p class="referencias" id="titulo-ref">Referencias</p>
    <p class="referencias"><u>Cantidad de Sandwiches</u>:  Días que se come en la facultad</p>
    <p class="referencias"><u>Relleno de Sandwiches</u>:  Preferencia de comida de tal lugar</p>
    <p class="referencias"><u>Longitud del plato</u>:  Rating del tostado de Mingo</p>
    <p class="referencias"><u>Mosquinha o brillitos</u>:  Calidad del servicio del lugar elegido</p>
    <p class="referencias"><u>Color Vaso Café</u>:  Preferencia de café de tal lugar</p>
    <p class="referencias"><u>Relleno vaso</u>:  Gasto promedio en comida</p>
  </div>
</main>


<style>
  #f_f{position:relative;right:525px; top: -500px}
  #f_m{position:relative;right:250px; top:-525px;}
  #f_g{position:relative;right:285px; top: -500px;}
  #f_r{position:relative;right:10px; top: -545px;}
  #f_h{position:relative;right:45px; top: -525px;}
  #f_c{position:relative;right:80px; top:-500px;}

  #p_f{position:relative; top:-530px; right:700px;}
  #p_m{position:relative; top:-680px; left:220px}
  #p_g{position:relative; top:-655px; left:172px;}
  #p_r{position:relative; top:-700px; left:400px;}
  #p_h{position:relative; top:-678px; left:325px;}
  #p_c{position:relative; top:-655px; left:260px;}

  .corchetes{
    display: flex;
    align-items: end;
    column-gap: 300px;
    position: relative;
    right: 50px;
    top:-140px;
  }
  .frecuencia{
    display:flex;
    column-gap: 260px;
    position:relative;
    right:80px;
    top:-250px;
  }
  .lineas_long{
    display:flex;
    flex-direction: row;
    align-items: center;
    column-gap: 300px;
    position: relative;
    top:-340px
  }
  .parrafos_punt{
    display:flex;
    column-gap: 160px;
    position:relative;
    left: 130px;
    top:-460px;
  }

  .servicio{
    display:flex;
    column-gap: 60px;
    position:relative;
    left:350px;
    bottom:580px
  }

  .preferencia_cafe{
    display:flex;
    column-gap: 180px;
    position:relative;
    left:450px;
    bottom: 320px
  }
  .container {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: start;
    flex-wrap: wrap;
    margin-left: 120px;
    width: 1020px;
    height: 1000px;
    background-color: rgba(32, 101, 37, 0.8);
    border:solid 5px rgba(80, 50, 1, 0.8);
  }
  h3{
   font-family: Homemade Apple; 
   font-size: 40px; 
   color: white; 
   position:relative;
   left:380px
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

  
  .sanguches_ref{
    display: flex;
    align-items: end;
    position:absolute;
    margin-top: 160px;
    margin-left: -100px;
    column-gap: 150px;
  }

  .platillos{
    display: flex;
    align-items: end;
    position:relative;
    column-gap: 192px;
    margin-top: 166px;
    right: 60px
    
  }
  .no_plato{
    margin-top: 40px;
    margin-left: 100px;
  }
  .plato{
    margin-top: 100px;
  }

   .cafe{
    display:flex;
    position: absolute;
    margin-top: 650px;
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
    left:90px;
    font-size:22px;
  }

  p{
    font-family: Satisfy;
    font-size: 20px;
    color:white;
    text-align: center;
  }

  .cont-ref{
    position:relative;
    bottom:400px;
    left: 200px
  }
  .referencias{
    text-align: start;
    line-height: .8px;
  }
  #titulo-ref{
    font-size:22px;
  }
</style>

  