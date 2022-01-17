## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/ABMiriam/ABMiriam.github.io/edit/main/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

<html>
    <head>
        <link rel="stylesheet" href="a.css">
        <title>&#10024; Tres en Raya &#10024;</title>
    </head>
    <body>
        <h1>3 en raya</h1>
        <div id="opciones">
            <div id="modos">
            <h3 id="modo">Elige el modo: </h3>
                    <h4 id="elegirModos1" onclick="elegirModo(this, 1)">Modo 6 fichas</h4>
                    <h4 id="elegirModos2" onclick="elegirModo(this, 2)">Modo 9 fichas</h4>
            </div>
            <div id="jugadores">
                <h3> Elige los jugadores: </h3>
                    <h4 id="elegirOpciones1" onclick="mostrar(this,'jj')" class="jugar">Jugador vs Jugador</h4>
                    <h4 id="elegirOpciones2" onclick="mostrar(this,'jo')" class="jugar">Jugador vs Ordenador</h4>
                    <!--<h4 id="elegirOpciones3" onclick="mostrar(this,'ji')" class="jugar">Jugador vs IA</h4>-->
            </div>
        </div>
        <br/>
        <h4 id="modalidad"></h4>
        <h4 id="tur">Turno de: <span id="turno"></span></h4>
        <div id="repe">
            <h3 onclick="repetir(this)"> Repetir </h3>
            <h3 onclick="volver(this)"> Empezar de nuevo </h3>
        </div>
        <div id="juego">
            <div id="contadores">
            <div id="fichas">
                <h3><span id="j1">Jugador</span> te quedan: <span id="fj1"></span> fichas</h3>
                <h3 id="jugador2"><span id="j2"></span> te quedan: <span id="fj2"></span> fichas</h3>
            </div>
            <div id=tiempos>
                <p>&#8986; Tiempo de juego: <span id="tiej"></span></p>
                <p>&#8987; Tiempo restante de jugada: <span id="tieres"></span> </p>
            </div>
            <div id="empatar">
                <h3 onclick="terminarModoSeis()">Terminar partida</h3>
            </div>
            </div>
            <div id="tablero">
                <table id="tablaUno">
                    <tr>
                        <td id="11" onmousedown="funcion(event, this, '11')"></td>
                        <td id="12" onmousedown="funcion(event, this, '12')"></td>
                        <td id="13" onmousedown="funcion(event, this, '13')"></td>
                    </tr>
                    <tr>
                        <td id="21" onmousedown="funcion(event, this, '21')"></td>
                        <td id="22" onmousedown="funcion(event, this, '22')"></td>
                        <td id="23" onmousedown="funcion(event, this, '23')"></td>
                    </tr>
                    <tr>
                        <td id="31" onmousedown="funcion(event, this, '31')"></td>
                        <td id="32" onmousedown="funcion(event, this, '32')"></td>
                        <td id="33" onmousedown="funcion(event, this, '33')"></td>
                    </tr>
                </table>
            </div>
            </div>
            <div id="ranking">
                    <h3>Histórico de partidas</h3>
                    <table id="contadorPartidas">
                        <tr>
                            <th colspan="3" id="uno" class="azul"></th>
                            <th colspan="3" id="dos" class="morado"></th>
                        </tr>
                        <tr>
                            <th class="azul">Ganadas</th>
                            <th class="azul">Empatadas</th>
                            <th class="azul">Perdidas</th>
                            <th class="morado">Ganadas</th>
                            <th class="morado">Empatadas</th>
                            <th class="morado">Perdidas</th>
                        </tr>
                        <tr>
                            <td id="ganadasJg1"></td>
                            <td id="empatadasJg1"></td>
                            <td id="perdidasJg1"></td>
                            <td id="ganadasJg2"></td>
                            <td id="empatadasJg2"></td>
                            <td id="perdidasJg2"></td>
                        </tr>
                    </table>
            </div>
        <script>
            
            let partida=[];
            let opcion;
            let modo;
            let terminar=false;
            let turj=6;
            let turjg1;
            let victoria=false;
            let jugadorwins=false;
            let cpuwins=false;
            let empatado=false;
            let reseteado=true;
            let contador=1;
            let fichas=6;
            let fichasj1=3;
            let fichasj2=3;
            let intjug;
            let intpar;
            let intjug2;
            let gj1=false;
            let restante;
            let cvjg1=0;
            let cvjg2=0;
            let victoriasJugador=0;
            let perdidasJugador=0;
            let victoriasOrdenador=0;
            let perdidasOrdenador=0;
            let empates=0;

            function iniciar (){
                document.getElementById("empatar").style.display="none";
                document.getElementById("ranking").style.visibility='hidden';
                document.getElementById("tiempos").style.visibility='hidden';
                document.getElementById("fichas").style.display='none';
                document.getElementById("repe").style.visibility='hidden';
                document.getElementById("tur").style.visibility='hidden';
                document.getElementById("tablero").style.visibility='hidden';
                document.getElementById("jugadores").style.visibility="hidden";
                for (let i=0; i<3;i++){
                    partida[i]=new Array();
                    for (let j=0; j<3;j++){
                        partida[i][j]=0;
                    }
                }
                console.log("Tarea realizada por: Miriam Almohalla");
            }
            function elegirModo (elem, op){
                if (op==1){
                    elem.style.color="plum";
                    document.getElementById("jugadores").style.visibility="visible";
                    opcion=1;
                }
                else if (op==2){
                    elem.style.color="plum";
                    document.getElementById("jugadores").style.visibility="visible";
                    opcion=2;
                }
            }
            function mostrar (elem, m){
                elem.style.color="plum";
                if (opcion==1){
                    document.getElementById("empatar").style.display="inline";
                    document.getElementById("fichas").style.display="inline";
                    document.getElementById("jugador2").style.visibility='visible';
                    if (m=="jj"){
                        document.getElementById("tur").style.visibility='visible';
                        document.getElementById("opciones").hidden=true;
                        document.getElementById("tablero").style.visibility='visible';
                        document.getElementById("modalidad").style.visibility='visible';
                        document.getElementById("modalidad").innerHTML="Has elegido la modalidad: jugador contra jugador con 6 fichas";
                        modo=1;
                        temporizadorPart();
                        temporizadorJug();
                        modojj();
                    }
                    else if (m=="jo"){
                        document.getElementById("tur").style.visibility='visible';
                        document.getElementById("modalidad").style.visibility='visible';
                        document.getElementById("modalidad").innerHTML="Has elegido la modalidad: jugador contra ordenador con 6 fichas";
                        document.getElementById("opciones").hidden=true;
                        document.getElementById("tablero").style.visibility='visible';
                        document.getElementById("jugador2").style.visibility='hidden';
                        modo=2;
                        temporizadorPart();
                        temporizadorJug();
                        turnos();
                        document.getElementById("fj1").innerHTML="3";
                    }
                    else if (m=="ji"){
                        document.getElementById("modalidad").style.visibility='visible';
                        document.getElementById("modalidad").innerHTML="Has elegido la modalidad: jugador contra IA con 6 fichas";
                        document.getElementById("opciones").hidden=true;
                        document.getElementById("tablero").style.visibility='visible';
                        modo=3;
                        temporizadorPart();
                        temporizadorJug();
                    }
                }
                else if(opcion==2){
                    if (m=="jj"){
                        document.getElementById("tur").style.visibility='visible';
                        document.getElementById("opciones").hidden=true;
                        document.getElementById("tablero").style.visibility='visible';
                        document.getElementById("modalidad").style.visibility='visible';
                        document.getElementById("modalidad").innerHTML="Has elegido la modalidad: jugador contra jugador con 9 fichas";
                        modo=1;
                        temporizadorPart();
                        temporizadorJug();
                        modojj(opcion,m);
                    }
                    else if (m=="jo"){
                        document.getElementById("tur").style.visibility='visible';
                        document.getElementById("modalidad").style.visibility='visible';
                        document.getElementById("modalidad").innerHTML="Has elegido la modalidad: jugador contra ordenador con 9 fichas";
                        document.getElementById("opciones").hidden=true;
                        document.getElementById("tablero").style.visibility='visible';
                        modo=2;
                        temporizadorPart();
                        temporizadorJug();
                        turnos();
                    }
                    else if (m=="ji"){
                        document.getElementById("modalidad").style.visibility='visible';
                        document.getElementById("modalidad").innerHTML="Has elegido la modalidad: jugador contra IA con 9 fichas";
                        document.getElementById("opciones").hidden=true;
                        document.getElementById("tablero").style.visibility='visible';
                        modo=3;
                        temporizadorPart();
                        temporizadorJug();
                    }
                }
            }
            function temporizadorPart(){
                document.getElementById("tiempos").style.visibility='visible';
                
                var contpar=0;
                var a=document.getElementById("tiej");
                    intpart=window.setInterval(function(){
                    if(contpar<60){
                        a.innerHTML=contpar+" segundos";
                    }
                    else if(contpar>60){
                        a.innerHTML=Math.floor(contpar/60)+" minutos "+Math.floor(contpar%60)+" segundos";
                    }
                    else if (contpar>3600){
                        a.innerHTML=Math.floor(contpar/3600)+" horas"+ Math.floor(contpar%3600)+" minutos ";
                    }
                    contpar++;
                    },1000);
            }
            function temporizadorJug(){
                    if (modo!=2){
                        restante=30;
                        var e= document.getElementById("tieres");//esta es para el segundo temporizador
                        intjug = window.setInterval(function(){
                            e.innerHTML=restante+" segundos";
                            restante--;
                            if (restante<=0){
                                alert("SE ACABÓ EL TIEMPO");
                                ganaOrdenador();
                                clearInterval(intjug);
                            }
                        },1000);
                    }
                    else if (modo==2){
                        restante=30;
                        var e= document.getElementById("tieres");//esta es para el segundo temporizador
                        intjug = window.setInterval(function(){
                            e.innerHTML=restante+" segundos";
                            restante--;
                            if (restante<=0 ){
                                alert("SE ACABÓ EL TIEMPO");
                                ganaOrdenador();
                                clearInterval(intjug);
                            }
                        },1000);
                    }
                    else if (modo==1 && !turjg1 ){
                        //aqui entra si el modo es jvsj y no es el turno de jg1
                        var e= document.getElementById("tieres");//esta es para el segundo temporizador
                        intjug2= window.setInterval(function(){
                            e.innerHTML=restante+" segundos";
                            restante--;
                            if (restante==0){
                                alert("SE ACABÓ EL TIEMPO");
                                ganaOrdenador();
                                clearInterval(intjug2);
                                gj1=true;
                            }
                        },1000);
                    }
            }
            function modojj(){
                jugador1=prompt("Introduce el nombre del jugador 1: ");
                jugador2=prompt("Introduce el nombre del jugador 2: ");
                turnos();
                if (opcion==1 && modo==1){
                    document.getElementById("j1").innerHTML=jugador1;
                    document.getElementById("j2").innerHTML=jugador2;
                    document.getElementById("fj1").innerHTML="3";
                    document.getElementById("fj2").innerHTML="3";

                }
                if(terminar==true){
                    document.getElementById("opciones").hidden=false;
                }
            }
            function turnos(){
                    //o 1=6f o 2 =9f
                if (opcion==1 && modo==1 && terminar==false){   
                    //6 fichas jugador contra jugador
                        if (contador%2!=0){
                            document.getElementById("turno").innerHTML=jugador1;
                            turjg1=true;
                        }
                        else if (contador%2==0 && turj>0) {
                            document.getElementById("turno").innerHTML=jugador2;
                            turjg1=false;
                        }  
                }
                else if (opcion==1 && modo==2 && terminar==false){
                    //6fichas jugador contra ordenador
                    if (terminar==false){
                        if (contador%2!=0){
                            document.getElementById("turno").innerHTML=" jugador";
                        }
                        else if (contador%2==0) {
                            document.getElementById("turno").innerHTML=" ordenador";
                            turnoOrd();
                        }
                    }
                }
                else if (opcion==2 && modo==1 && terminar==false){
                    //9 fichas jugador contra jugador
                    //comprobarEmpate();
                        if (contador%2!=0){
                            document.getElementById("turno").innerHTML=jugador1;
                            turjg1=true;
                            comprobarEmpate();
                        }
                        else if (contador%2==0 && turj>0) {
                            document.getElementById("turno").innerHTML=jugador2;
                            turjg1=false;
                            comprobarEmpate();
                        }  
                }
                else if (opcion==2 && modo==2 && terminar==false){
                    //9 fichas jugador contra ordenador
                    if (terminar==false){
                        if (contador%2!=0){
                            document.getElementById("turno").innerHTML=" jugador";
                            comprobarEmpate();
                            turj--;
                        }
                        else if (contador%2==0 && turj>0) {
                            document.getElementById("turno").innerHTML=" ordenador";
                            comprobarEmpate();
                            turnoOrd();
                        }
                    }
                }
            }
            function turnoOrd(){
                if (opcion==1 && modo==2){
                    let vacio=false;
                    let volverAPoner;
                    while (vacio!=true && terminar==false){
                        if (!reseteado && fichasj2>0){
                            ordi=Math.floor(Math.random()*3);
                            ordj=Math.floor(Math.random()*3);
                            if (volverAPoner){
                                while (ordi==borradoi && ordj==borradoj){
                                    ordi=Math.floor(Math.random()*3);
                                }
                                volverAPoner=false;
                            }
                            posi=String(ordi+1);
                            posj=String(ordj+1);
                            pos=posi+posj;
                            if (partida[ordi][ordj]==0){
                                partida[ordi][ordj]=2;
                                contador++;
                                fichasj2--;
                                vacio=true;
                                document.getElementById(pos).style.backgroundColor="plum";
                            }
                        }
                        else if (!reseteado && fichasj2==0){
                            let fichasOrd=[];
                            let borrar=Math.floor(Math.random()*3+1);
                            //borrar elige aleatoriamente que ficha va a cambiar le ordenador.
                            //voy a recorrer partida para conseguir todas las posiciones en las que el ordenador tiene ficha.
                                for (let i=0; i<partida.length;i++){
                                    for(let j=0; j<partida.length;j++){
                                        if (partida[i][j]==2){
                                            fichasOrd.push(i,j);
                                        }
                                    }
                                }
                            switch (borrar){
                                case 1:
                                    posi=fichasOrd[0];
                                    posj=fichasOrd[1];
                                    break;
                                case 2: 
                                    posi=fichasOrd[2];
                                    posj=fichasOrd[3];
                                    break;
                                case 3:
                                    posi=fichasOrd[4];
                                    posj=fichasOrd[5];
                                break;
                            }
                            borradoi=posi;
                            borradoj=posj;
                            partida[posi][posj]=0;
                            posi++;
                            posj++;
                            posn=String(posi)+String(posj);
                            document.getElementById(posn).style.backgroundColor="transparent";
                            fichasj2++;
                            volverAPoner=true;
                        }
                        else {
                            break;
                        }
                    }
                    comprobarGanacionORDENADOR();
                    turnos();
                }
                if (opcion==2 && modo==2){
                    let vacio=false;
                    while (vacio!=true && terminar==false){
                        if (!reseteado){
                            ordi=Math.floor(Math.random()*3+1);
                            ordj=Math.floor(Math.random()*3+1);
                            posi=String(ordi);
                            posj=String(ordj);
                            pos=posi+posj;
                            ordi=ordi-1;
                            ordj=ordj-1;
                            if (partida[ordi][ordj]==0){
                                partida[ordi][ordj]=2;
                                contador++;
                                vacio=true;
                                document.getElementById(pos).style.backgroundColor="plum";
                            }
                        }
                        else {
                            break;
                        }
                    }
                    comprobarGanacionORDENADOR();
                    turnos();
                }
            }
            function funcion (event, elem, id){
                if (opcion==1 && modo==1){
                    c=id.split();
                    posi=parseInt(id[0]-1);
                    posj=parseInt(id[1]-1);
                    quitadaj1=true;
                    if (fichasj1==0){
                        quitadaj1=false;
                    }
                    else {
                        quitadaj1=true;
                    }
                    if (fichasj2==0){
                        quitadaj2=false;
                    }
                    else {
                        quitadaj2=true;
                    }
                    if (turjg1 && fichasj1>0 && partida[posi][posj]!=1 && partida[posi][posj]!=2){
                        clearInterval(intjug);
                        clearInterval(intjug2);
                        temporizadorJug();
                        contador++;
                        if (event.button==0 && partida[posi][posj]==0){
                            elem.style.backgroundColor="cornflowerblue";
                            partida[posi][posj]=1;
                            reseteado=false;
                            fichasj1--;
                            document.getElementById("fj1").innerHTML=fichasj1;
                        }
                        comprobarGanacionJUGADOR();
                        turnos();
                    }
                    else if (!quitadaj1 && turjg1 && event.button==2 && partida[posi][posj]==1){
                            quitadaj1=true;
                            elem.style.backgroundColor="transparent";
                            partida[posi][posj]=0;
                            fichasj1++;
                            document.getElementById("fj1").innerHTML=fichasj1;
                    }
                    else if (turjg1 && fichasj1<=0){
                        alert(jugador1+" TE HAS QUEDADO SIN FICHAS QUITA ALGUNA");
                    }
                    //jugador2
                    if (!turjg1 && fichasj2>0 && partida[posi][posj]!=1 && partida[posi][posj]!=2){
                        contador++;
                        if (event.button==0 && partida[posi][posj]==0){
                            elem.style.backgroundColor="plum";
                            clearInterval(intjug);
                            clearInterval(intjug2);
                            temporizadorJug();
                            partida[posi][posj]=2;
                            reseteado=false;
                            fichasj2--;
                            document.getElementById("fj2").innerHTML=fichasj2;
                        }
                        comprobarGanacionORDENADOR();
                        turnos();
                    }
                    else if (!quitadaj2 && !turjg1 && event.button==2 && partida[posi][posj]==2){
                            quitadaj2=true;
                            elem.style.backgroundColor="transparent";
                            partida[posi][posj]=0;
                            fichasj2++;
                            document.getElementById("fj2").innerHTML=fichasj2;
                    }
                    else if (!turjg1 && fichasj2<=0){
                        alert(jugador2+" TE HAS QUEDADO SIN FICHAS QUITA ALGUNA");
                    } 
                }
                else if (opcion==1 && modo==2){
                    c=id.split();
                    posi=parseInt(id[0]-1);
                    posj=parseInt(id[1]-1);
                    quitada=true;
                    if (fichasj1==0){
                        quitada=false;
                    }
                    else {
                        quitada=true;
                    }
                    if (fichasj1>0 && partida[posi][posj]!=1 && partida[posi][posj]!=2){
                        if (event.button==0 && partida[posi][posj]==0){
                            clearInterval(intjug);
                            clearInterval(intjug2);
                            temporizadorJug();
                            elem.style.backgroundColor="cornflowerblue";
                            partida[posi][posj]=1;
                            contador++;
                            reseteado=false;
                            fichasj1--;
                            document.getElementById("fj1").innerHTML=fichasj1;
                        }
                        comprobarGanacionJUGADOR();
                    }
                    else if (!quitada && event.button==2 && partida[posi][posj]==1){
                            quitada=true;
                            elem.style.backgroundColor="transparent";
                            partida[posi][posj]=0;
                            fichasj1++;
                            document.getElementById("fj1").innerHTML=fichasj1;
                    }
                    else if (fichasj1<=0){
                        alert("JUGADOR TE HAS QUEDADO SIN FICHAS QUITA ALGUNA");
                    }
                    turnos();
                }
                else if (opcion==2 && modo==1){
                    c=id.split();
                    posi=parseInt(id[0]-1);
                    posj=parseInt(id[1]-1);
                    if (turjg1 && partida[posi][posj]!=1 && partida[posi][posj]!=2){
                        reseteado=false;
                        elem.style.backgroundColor="cornflowerblue";
                        clearInterval(intjug);
                        clearInterval(intjug2);
                        temporizadorJug();
                        partida[posi][posj]=1;
                        contador++;
                        comprobarGanacionJUGADOR();
                        turnos();
                    }
                    else if (turjg1==false && partida[posi][posj]!=1 && partida[posi][posj]!=2){
                        c=id.split();
                        posi=parseInt(id[0]-1);
                        posj=parseInt(id[1]-1);
                        if (partida[posi][posj]!=1 && partida[posi][posj]!=2){
                            reseteado=false;
                            elem.style.backgroundColor="plum";
                            clearInterval(intjug);
                            clearInterval(intjug2);
                            temporizadorJug();
                            partida[posi][posj]=2;
                            contador++;
                            comprobarGanacionORDENADOR();
                            turnos();
                        }
                    }

                }
                else if (opcion==2 && modo==2){
                    c=id.split();
                    posi=parseInt(id[0]-1);
                    posj=parseInt(id[1]-1);
                    if (partida[posi][posj]==0){
                        elem.style.backgroundColor="cornflowerblue";
                            partida[posi][posj]=1;
                            clearInterval(intjug);
                            clearInterval(intjug2);
                            temporizadorJug();
                            reseteado=false;
                            fichas--;
                            contador++;
                            comprobarGanacionJUGADOR();
                            turnos();
                    }
                }
            }
            function comprobarEmpate(){
                if (victoria==false && contador>9){
                    terminar=true;
                    empatado=true;
                    empates++;
                    alert("EMPATE. Partida terminada");
                    finalPartida();
                }
            }
            function comprobarGanacionJUGADOR() {
                if (partida[0][0]==1 && partida[0][1]==1 && partida[0][2]==1){
                    ganaJugador();
                }
                else if (partida[1][0]==1 && partida[1][1]==1 && partida[1][2]==1){
                    ganaJugador();
                }
                else if (partida[2][0]==1 && partida[2][1]==1 && partida[2][2]==1){
                    ganaJugador();
                }
                else if (partida[0][0]==1 && partida[1][1]==1 && partida[2][2]==1){
                    ganaJugador();
                }
                else if (partida[0][2]==1 && partida[1][1]==1 && partida[2][0]==1){
                    ganaJugador();
                }
                else if (partida[0][2]==1 && partida[1][1]==1 && partida[2][0]==1){
                    ganaJugador();
                }
                else if (partida[0][0]==1 && partida[1][0]==1 && partida[2][0]==1){
                    ganaJugador();
                }
                else if (partida[0][1]==1 && partida[1][1]==1 && partida[2][1]==1){
                    ganaJugador();
                }
                else if (partida[0][2]==1 && partida[1][2]==1 && partida[2][2]==1){
                    ganaJugador();
                }
            }
            function comprobarGanacionORDENADOR() {
                if (partida[0][0]==2 && partida[0][1]==2 && partida[0][2]==2){
                    ganaOrdenador();
                }
                else if (partida[1][0]==2 && partida[1][1]==2 && partida[1][2]==2){
                    ganaOrdenador();
                }
                else if (partida[2][0]==2 && partida[2][1]==2 && partida[2][2]==2){
                    ganaOrdenador();
                }
                else if (partida[0][0]==2 && partida[1][1]==2 && partida[2][2]==2){
                    ganaOrdenador();
                }
                else if (partida[0][2]==2 && partida[1][1]==2 && partida[2][0]==2){
                    ganaOrdenador();
                }
                else if (partida[0][0]==2 && partida[1][0]==2 && partida[2][0]==2){
                    ganaOrdenador();
                }
                else if (partida[1][0]==2 && partida[1][1]==2 && partida[1][2]==2){
                    ganaOrdenador();
                }
                else if (partida[2][0]==2 && partida[2][1]==2 && partida[2][2]==2){
                    ganaOrdenador();
                }
                else if (partida[0][2]==2 && partida[1][2]==2 && partida[2][2]==2){
                    ganaOrdenador();
                }
                else if (partida[0][0]==2 && partida[1][0]==2 && partida[2][0]==2){
                    ganaOrdenador();
                }
                else if (partida[0][1]==2 && partida[1][1]==2 && partida[2][1]==2){
                    ganaOrdenador();
                }
                else if (partida[2][0]==2 && partida[2][1]==2 && partida[2][2]==2){
                    ganaOrdenador();
                }
            }
            function ganaJugador(){
                terminar=true;
                victoria=true;
                jugadorwins=true;
                victoriasJugador++;
                perdidasOrdenador++;
                if(modo==2){
                    alert ("JUGADOR HA GANADO");
                    finalPartida();
                }
                else if (modo==1){
                    alert ("HA GANADO: "+jugador1);
                    finalPartida();
                }
            }
            function ganaOrdenador(){
                terminar=true;
                victoria=true;
                cpuwins=true;
                victoriasOrdenador++;
                perdidasJugador++;
                if (modo==2){
                    alert ("ORDENADOR HA GANADO");
                    finalPartida();
                }
                else if (modo==1 && !gj1){
                    alert ("HA GANADO: "+jugador2);
                    finalPartida();
                }
                else if (modo==1 && gj1==true){
                    alert ("HA GANADO: "+jugador1);
                    finalPartida();
                }
            }
            function finalPartida(){
                clearInterval(intjug);
                clearInterval(intjug2);
                clearInterval(intpart);
                ranking();
                document.getElementById("empatar").style.display="none";
                document.getElementById("tiempos").style.visibility='hidden';
                document.getElementById("jugador2").style.visibility='hidden';
                document.getElementById("fichas").style.display='none';
                document.getElementById("repe").style.visibility='visible';
                document.getElementById("tablero").style.visibility='hidden';
                document.getElementById("modalidad").style.visibility='hidden';
                document.getElementById("tur").style.visibility='hidden';
                document.getElementById("tur").style.visibility='hidden';
                document.getElementById("elegirModos1").style.color="black";
                document.getElementById("elegirModos2").style.color="black";
                document.getElementById("elegirOpciones1").style.color="black";
                document.getElementById("elegirOpciones2").style.color="black";
            }
            function repetir(elem){
                resetrepe();
                document.getElementById("repe").style.visibility='hidden';
                document.getElementById("tur").style.visibility='visible';
                document.getElementById("modalidad").style.visibility='visible';
                document.getElementById("opciones").hidden=true;
                document.getElementById("tablero").style.visibility='visible';
                document.getElementById("fichas").style.display="inline";
                document.getElementById("fj1").innerHTML="3";
                temporizadorPart();
                temporizadorJug();
                turnos();
            }
            function volver(elem){
                reset();
                document.getElementById("repe").style.visibility='hidden';
                document.getElementById("opciones").hidden=false;
                document.getElementById("modos").style.visibility='visible';
                document.getElementById("jugadores").style.visibility='hidden';
            }
            function resetrepe(){
                for (let i=0; i<partida.length;i++){
                    for (let j=0; j<partida.length; j++){
                        posi=i+1;
                        posj=j+1;
                        pos=posi.toString()+posj.toString();
                        document.getElementById(pos).style.backgroundColor="transparent";
                    }
                }
                for (let i=0; i<3;i++){
                    partida[i]=new Array();
                    for (let j=0; j<3;j++){
                        partida[i][j]=0;
                    }
                }
                contador=1;
                victoria=false;
                turj=6;
                terminar=false;
                jugadorwins=false;
                cpuwins=false;
                empatado=false;
                reseteado=true;
                fichasj1=3;
                fichasj2=3;
                intjug=0;
                intpar=0;
                intjug2=0;
                gj1=false;
            }
            function reset(){
                for (let i=0; i<partida.length;i++){
                    for (let j=0; j<partida.length; j++){
                        posi=i+1;
                        posj=j+1;
                        pos=posi.toString()+posj.toString();
                        document.getElementById(pos).style.backgroundColor="transparent";
                    }
                }
                for (let i=0; i<3;i++){
                    partida[i]=new Array();
                    for (let j=0; j<3;j++){
                        partida[i][j]=0;
                    }
                }
                
                cvjg1=0;
                cvjg2=0;
                contador=1;
                victoria=false;
                turj=6;
                terminar=false;
                jugadorwins=false;
                cpuwins=false;
                empatado=false;
                reseteado=true;
                modo=0;
                opcion=0;
                jugador1="";
                jugador2="";
                fichasj1=3;
                fichasj2=3;
                intjug=0;
                intpar=0;
                intjug2=0;
                gj1=false;
                victoriasJugador=0;
                perdidasJugador=0;
                victoriasOrdenador=0;
                perdidasOrdenador=0;
                empates=0;
                limpiarRanking();
            }
            function ranking (){
                document.getElementById("ranking").style.visibility='visible';
                if (modo==2){
                    document.getElementById("uno").innerHTML="Jugador";
                    document.getElementById("dos").innerHTML="Ordenador";
                }
                else if (modo==1){
                    document.getElementById("uno").innerHTML=jugador1;
                    document.getElementById("dos").innerHTML=jugador2;
                }
                document.getElementById("ganadasJg1").innerHTML=victoriasJugador;
                document.getElementById("ganadasJg2").innerHTML=victoriasOrdenador;
                document.getElementById("empatadasJg1").innerHTML=empates;
                document.getElementById("empatadasJg2").innerHTML=empates;
                document.getElementById("perdidasJg1").innerHTML=perdidasJugador;
                document.getElementById("perdidasJg2").innerHTML=perdidasOrdenador;
            }
            function limpiarRanking(){
                document.getElementById("ranking").style.visibility='hidden';
                document.getElementById("uno").innerHTML="";
                document.getElementById("dos").innerHTML="";
            }
            function terminarModoSeis(){
                victoria=false;
                contador=26;
                comprobarEmpate();
            }
            iniciar();
            
        </script>
    </body>
</html>
