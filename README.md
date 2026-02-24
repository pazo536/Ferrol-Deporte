<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>Ferrol Deporte - Noticias y Clasificación Real</title>
<style>
body, h1,h2,h3,p,ol,li { margin:0; padding:0; box-sizing:border-box; }
body { font-family: 'Arial Black', Arial, sans-serif; background:#fff; color:#000; }
a { text-decoration:none; color:inherit; }
header { display:flex; justify-content:space-between; align-items:center; padding:1rem; background:#004d00; position:sticky; top:0; z-index:1000; box-shadow:0 2px 5px rgba(0,0,0,0.2);}
nav a { margin:0 0.5rem; color:#fff; font-weight:bold; cursor:pointer; transition:0.2s; }
nav a:hover { color:#ffd700; }
.logo { font-size:2.5rem; font-weight:bold; color:#fff; background:#228B22; padding:0.2rem 0.5rem; border-radius:5px; box-shadow:0 2px 4px rgba(0,0,0,0.3); }
.hero { margin:1rem 0; border-radius:8px; overflow:hidden; position:relative; transition:all 0.5s ease; }
.hero img { width:100%; max-height:350px; object-fit:cover; display:block; border-radius:8px; transition: all 0.5s ease; }
.hero.animar img { transform:scale(1.05); opacity:0.8; }
.hero h1 { font-size:28px; margin:0.5rem; position:absolute; bottom:60px; left:20px; color:#fff; text-shadow:2px 2px 6px #000; transition:all 0.5s ease; }
.hero p { font-size:16px; margin:0.5rem 20px 20px 20px; position:absolute; bottom:20px; left:0; color:#fff; text-shadow:1px 1px 4px #000; transition:all 0.5s ease; }
.main { display:flex; gap:1rem; margin:1rem; flex-wrap:wrap; }
.sidebar { width:240px; background:#f0f0f0; padding:1rem; border-radius:6px; box-shadow:0 1px 6px rgba(0,0,0,0.1); height:max-content; position:sticky; top:80px; }
.sidebar h2 { margin-top:0; font-size:18px; border-bottom:1px solid #ccc; padding-bottom:0.5rem; color:#000; }
.sidebar ol { margin:0; padding-left:20px; }
.sidebar li { margin:0.5rem 0; font-size:14px; opacity:0.6; transition:all 0.3s; cursor:pointer; }
.sidebar li:hover { opacity:1; transform:scale(1.02); }
.sidebar li.racing { font-weight:bold; color:#228B22; font-size:16px; opacity:1; }
@keyframes parpadeo {
  0%,100% { opacity:1; }
  25%,75% { opacity:0.2; }
  50% { opacity:1; }
}
.listado { flex:1; display:grid; grid-template-columns:repeat(auto-fit,minmax(300px,1fr)); gap:1rem; }
.listado article { background:#f9f9f9; padding:1rem; border-radius:6px; box-shadow:0 1px 3px rgba(0,0,0,0.1); transition:0.5s; cursor:pointer; display:flex; flex-direction:column; opacity:0; transform:translateY(20px);}
.listado article.visible { opacity:1; transform:translateY(0);}
.listado article:hover { transform:translateY(-5px) scale(1.02); box-shadow:0 4px 10px rgba(0,0,0,0.15);}
.listado h3 { margin:0 0 0.5rem 0; font-size:16px; color:#000;}
.listado p { margin:0 0 0.5rem 0; font-size:14px; color:#333; }
.listado .medio { font-size:12px; color:#555; display:flex; align-items:center; gap:4px; margin-top:auto; }
.listado .medio img { height:16px; border-radius:2px; }
.listado img.noticia { width:100%; height:150px; object-fit:cover; border-radius:6px; margin-bottom:0.5rem; }
.modal { position:fixed; top:0; left:0; width:100%; height:100%; background:rgba(0,0,0,0.75); display:none; justify-content:center; align-items:center; z-index:10000; }
.modal-content { background:#fff; padding:1rem; border-radius:8px; max-width:600px; max-height:80%; overflow-y:auto; position:relative; color:#000; }
.modal-content h2 { margin-top:0; color:#000; }
.modal-close { position:absolute; top:0.5rem; right:0.5rem; cursor:pointer; font-weight:bold; color:#000; font-size:24px; }
footer { text-align:center; padding:1rem; font-size:12px; color:#555; }
</style>
</head>
<body>

<header>
  <div class="logo"><span>F</span>errol <span>D</span>eporte</div>
  <nav>
    <a href="#">Portada</a>
    <a href="#">Partidos</a>
    <a href="#">Fichajes</a>
    <a href="#">Club</a>
  </nav>
</header>

<section class="hero" id="hero">
  <img src="https://via.placeholder.com/1200x350/228B22/ffffff?text=Racing+de+Ferrol" alt="Hero">
  <h1 id="hero-titulo">Cargando noticia principal...</h1>
  <p id="hero-resumen"></p>
</section>

<div class="main">
  <aside class="sidebar">
    <h2>Clasificación</h2>
    <ol id="clasificacion">
      <li>Cargando...</li>
    </ol>
  </aside>

  <section class="listado" id="listado"></section>
</div>

<div class="modal" id="modal">
  <div class="modal-content">
    <span class="modal-close" onclick="cerrarModal()">×</span>
    <h2 id="modal-titulo"></h2>
    <p id="modal-resumen"></p>
    <span id="modal-medio"></span>
  </div>
</div>

<footer>
  © 2026 Ferrol Deporte | Noticias y clasificación en vivo
</footer>

<script>
const NEWSAPI_KEY = "7946d32466614bd6872927ca4c3b1661";
const API_FOOTBALL_KEY = "1569c47c3b3119876a3cc85a6b7c9157";

let pagina=1, cargando=false, ultimaPosicion=null;

async function cargarNoticias(){
  if(cargando) return;
  cargando=true;
  try{
    const res = await fetch(`https://newsapi.org/v2/everything?q=Racing+de+Ferrol&language=es&pageSize=5&page=${pagina}&sortBy=publishedAt&apiKey=${NEWSAPI_KEY}`);
    const data = await res.json();
    const listado = document.getElementById('listado');
    data.articles.forEach((n,i)=>{
      const art = document.createElement('article');
      let html='';
      if(n.urlToImage) html+=`<img src="${n.urlToImage}" class="noticia" alt="${n.title}">`;
      html+=`<h3>${n.title}</h3><p>${n.description||''}</p>`;
      html+=`<span class="medio">${n.source.name} <img src="https://via.placeholder.com/16x16?text=${n.source.name.charAt(0)}" alt="${n.source.name}"></span>`;
      art.innerHTML=html;
      art.onclick=()=>abrirModal({titulo:n.title,resumen:n.description||'',medio:n.source.name});
      listado.appendChild(art);
      setTimeout(()=>{art.classList.add('visible');},50);
      if(pagina===1 && i===0){
        actualizarHero(n);
      }
    });
    pagina++;
    cargando=false;
  }catch(e){ console.error(e); cargando=false;}
}

function actualizarHero(n){
  const hero = document.getElementById('hero');
  const img = hero.querySelector('img');
  const h1 = document.getElementById('hero-titulo');
  const p = document.getElementById('hero-resumen');
  img.src=n.urlToImage||"https://via.placeholder.com/1200x350/228B22/ffffff?text=Racing+de+Ferrol";
  h1.innerText=n.title;
  p.innerText=n.description||'';
  hero.classList.remove('animar');
  void hero.offsetWidth; // reinicia animación
  hero.classList.add('animar');
}

async function cargarClasificacion(){
  try{
    const res = await fetch("https://v3.football.api-sports.io/standings?league=408&season=2025",{
      headers: { "x-apisports-key": API_FOOTBALL_KEY }
    });
    const data = await res.json();
    const tabla = data.response[0].league.standings[0];
    const list = document.getElementById('clasificacion');
    list.innerHTML='';
    tabla.forEach((eq,index)=>{
      const li = document.createElement('li');
      if(eq.team.name==="Racing de Ferrol"){
        li.className='racing';
        li.innerHTML=`<strong style="color:#228B22">${eq.team.name} (${eq.points} pts)</strong>`;
        if(ultimaPosicion===null || ultimaPosicion!==index){
          li.style.animation='parpadeo 1.5s ease-in-out 0s 3';
          ultimaPosicion=index;
        }
      } else {
        li.textContent=`${eq.team.name} (${eq.points} pts)`;
      }
      list.appendChild(li);
    });
  }catch(e){ console.error(e); document.getElementById('clasificacion').innerHTML='<li>Error cargando clasificación</li>';}
}

window.addEventListener('scroll', ()=>{
  if(window.innerHeight + window.scrollY >= document.body.offsetHeight - 200){
    cargarNoticias();
  }
});

const modal=document.getElementById('modal');
function abrirModal(n){
  document.getElementById('modal-titulo').innerText=n.titulo;
  document.getElementById('modal-resumen').innerText=n.resumen;
  document.getElementById('modal-medio').innerHTML=n.medio;
  modal.style.display='flex';
}
function cerrarModal(){ modal.style.display='none';}

cargarNoticias();
cargarClasificacion();
setInterval(cargarClasificacion,60000);
</script>
</body>
</html>
