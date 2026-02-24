<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>Ferrol Deporte - Noticias y Clasificación</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
body, h1,h2,h3,p,ol,li { margin:0; padding:0; box-sizing:border-box; }
body { font-family:'Arial Black', Arial, sans-serif; background:#fff; color:#000; }
a { text-decoration:none; color:inherit; }

header {
  display:flex; justify-content:space-between; align-items:center;
  padding:1rem; background:#004d00; position:sticky; top:0; z-index:1000;
  box-shadow:0 2px 5px rgba(0,0,0,0.2);
}
.logo {
  font-size:2.5rem; font-weight:bold; color:#fff; background:#228B22;
  padding:0.2rem 0.5rem; border-radius:5px; text-shadow: 0 0 5px gold;
  animation:brillo 2s infinite alternate;
}
@keyframes brillo {
  0% { text-shadow: 0 0 5px gold, 0 0 10px gold; }
  50% { text-shadow: 0 0 10px gold, 0 0 20px gold; }
  100% { text-shadow: 0 0 5px gold, 0 0 10px gold; }
}
.header-right { text-align:right; color:#ffd700; font-weight:bold; font-size:14px; }

.hero { margin:1rem 0; border-radius:8px; overflow:hidden; position:relative; transition:all 0.5s ease; }
.hero img { width:100%; max-height:250px; object-fit:cover; display:block; border-radius:8px; }
.hero h1 { font-size:20px; position:absolute; bottom:50px; left:15px; color:#fff; text-shadow:2px 2px 6px #000; }
.hero p { font-size:14px; position:absolute; bottom:15px; left:15px; color:#fff; text-shadow:1px 1px 4px #000; }

.main { display:flex; gap:1rem; margin:1rem; flex-wrap:wrap; }
.sidebar { width:240px; background:#f0f0f0; padding:1rem; border-radius:6px; box-shadow:0 1px 6px rgba(0,0,0,0.1); height:max-content; position:sticky; top:80px; }
.sidebar h2 { margin-top:0; font-size:18px; border-bottom:1px solid #ccc; padding-bottom:0.5rem; color:#000; }
.sidebar ol { margin:0; padding-left:20px; }
.sidebar li { margin:0.5rem 0; font-size:14px; opacity:0.6; transition:all 0.3s; cursor:pointer; }
.sidebar li:hover { opacity:1; transform:scale(1.02); }
.sidebar li.racing { font-weight:bold; color:#228B22; font-size:16px; opacity:1; animation:parpadeo 1.5s ease-in-out 0s 3; }
@keyframes parpadeo {0%,100%{opacity:1;}25%,75%{opacity:0.2;}50%{opacity:1;}}

.listado { flex:1; display:grid; grid-template-columns:1fr; gap:1rem; }
.listado article { background:#f9f9f9; padding:1rem; border-radius:6px; box-shadow:0 1px 3px rgba(0,0,0,0.1); transition:0.5s; cursor:pointer; display:flex; flex-direction:column; opacity:1; }
.listado h3 { margin:0 0 0.5rem 0; font-size:16px; color:#000;}
.listado p { margin:0 0 0.5rem 0; font-size:14px; color:#333; }
.listado .medio { font-size:12px; color:#555; display:flex; align-items:center; gap:4px; margin-top:auto; }
.listado .medio img { height:16px; border-radius:2px; }
.listado img.noticia { width:100%; height:150px; object-fit:cover; border-radius:6px; margin-bottom:0.5rem; }

.modal { position:fixed; top:0; left:0; width:100%; height:100%; background:rgba(0,0,0,0.75); display:none; justify-content:center; align-items:center; z-index:10000; }
.modal-content { background:#fff; padding:1rem; border-radius:8px; max-width:90%; max-height:80%; overflow-y:auto; position:relative; color:#000; }
.modal-content h2 { margin-top:0; color:#000; }
.modal-close { position:absolute; top:0.5rem; right:0.5rem; cursor:pointer; font-weight:bold; color:#000; font-size:24px; }

footer { text-align:center; padding:1rem; font-size:12px; color:#555; }

@media(max-width:768px){
  .main{flex-direction:column;}
  .sidebar{width:100%; position:relative; top:auto;}
  .hero h1{font-size:18px; bottom:45px;}
  .hero p{font-size:12px; bottom:10px;}
}
</style>
</head>
<body>

<header>
  <div class="logo"><span>F</span>errol <span>D</span>eporte</div>
  <div class="header-right" id="ultima-actualizacion">Última actualización: --:--</div>
</header>

<section class="hero" id="hero">
  <img src="https://via.placeholder.com/1200x250/228B22/ffffff?text=Racing+de+Ferrol" alt="Hero">
  <h1 id="hero-titulo">Noticia principal de prueba</h1>
  <p id="hero-resumen">Resumen de la noticia principal para previsualización.</p>
</section>

<div class="main">
  <aside class="sidebar">
    <h2>Clasificación</h2>
    <ol id="clasificacion">
      <li class="racing">Racing de Ferrol (42 pts)</li>
      <li>Otro equipo (40 pts)</li>
      <li>Equipo 3 (38 pts)</li>
      <li>Equipo 4 (36 pts)</li>
      <li>Equipo 5 (34 pts)</li>
    </ol>
  </aside>

  <section class="listado" id="listado">
    <article>
      <img src="https://via.placeholder.com/600x150/228B22/ffffff?text=Noticia+1" class="noticia" alt="Noticia 1">
      <h3>Noticia de prueba 1</h3>
      <p>Resumen de la noticia 1 para ver el diseño de la web.</p>
      <span class="medio">Diario Ejemplo <img src="https://via.placeholder.com/16x16?text=D"></span>
    </article>
    <article>
      <img src="https://via.placeholder.com/600x150/228B22/ffffff?text=Noticia+2" class="noticia" alt="Noticia 2">
      <h3>Noticia de prueba 2</h3>
      <p>Resumen de la noticia 2 para ver el diseño de la web.</p>
      <span class="medio">Periódico Test <img src="https://via.placeholder.com/16x16?text=P"></span>
    </article>
  </section>
</div>

<div class="modal" id="modal">
  <div class="modal-content">
    <span class="modal-close" onclick="cerrarModal()">×</span>
    <h2 id="modal-titulo"></h2>
    <p id="modal-resumen"></p>
    <span id="modal-medio"></span>
  </div>
</div>

<footer>© 2026 Ferrol Deporte | Noticias y clasificación en vivo</footer>

<script>
const NEWSAPI_KEY="7946d32466614bd6872927ca4c3b1661";
const API_FOOTBALL_KEY="1569c47c3b3119876a3cc85a6b7c9157";

function actualizarHora(){
  const ahora=new Date();
  const h=String(ahora.getHours()).padStart(2,'0');
  const m=String(ahora.getMinutes()).padStart(2,'0');
  document.getElementById('ultima-actualizacion').innerText=`Última actualización: ${h}:${m}`;
}

// Modal
const modal=document.getElementById('modal');
function abrirModal(n){
  document.getElementById('modal-titulo').innerText=n.titulo;
  document.getElementById('modal-resumen').innerText=n.resumen;
  document.getElementById('modal-medio').innerHTML=n.medio;
  modal.style.display='flex';
}
function cerrarModal(){ modal.style.display='none'; }

actualizarHora();
setInterval(actualizarHora,60000);
</script>
</body>
</html>