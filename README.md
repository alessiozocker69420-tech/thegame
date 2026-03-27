<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<title>the game</title>

<style>
:root {
  --main:#00ffcc;
}

body {
  margin:0;
  font-family:Arial;
  background:#020617;
  color:white;
  text-align:center;
}

header {
  font-size:40px;
  padding:20px;
  background:linear-gradient(90deg,#00ffcc,#22c55e);
  -webkit-background-clip:text;
  color:transparent;
}

.btn {
  margin:5px;
  padding:10px;
  border:none;
  border-radius:10px;
  background:#111;
  color:var(--main);
  cursor:pointer;
}

#games {
  display:flex;
  flex-wrap:wrap;
  justify-content:center;
}

.game {
  width:200px;
  margin:10px;
  background:#111;
  border-radius:15px;
  cursor:pointer;
}

.game img {width:100%;}

/* WINDOWS */
.window {
  display:none;
  position:fixed;
  top:5%;
  left:5%;
  width:90%;
  height:85%;
  background:black;
  border:2px solid var(--main);
  border-radius:15px;
}

.window iframe {
  width:100%;
  height:100%;
}

.close {
  position:absolute;
  top:10px;
  right:10px;
  background:red;
  border:none;
  color:white;
  padding:8px;
  cursor:pointer;
}

</style>
</head>

<body>

<header>🎮 the game</header>

<div>
  <!-- FILTER -->
  <button class="btn" onclick="app.filter('all')">Alle</button>
  <button class="btn" onclick="app.filter('racing')">🚗 Racing</button>
  <button class="btn" onclick="app.filter('action')">🔫 Action</button>

  <!-- SORT -->
  <button class="btn" onclick="app.sortAZ()">A-Z</button>

  <br>
  <input id="search" placeholder="🔍 Suche...">
</div>

<div id="games"></div>

<!-- GAME WINDOW -->
<div id="gameWindow" class="window">
  <button class="close" onclick="app.closeGame()">❌</button>
  <iframe id="player"></iframe>
</div>

<script>

class App {

constructor(){
this.games=[

{title:"Ultimate Car Driving Simulator",category:"racing",url:"https://www.madkidgames.com/full/ultimate-car-driving-simulator",image:"https://via.placeholder.com/200"},
{title:"Airport Sniper",category:"action",url:"https://cdn.htmlgames.com/AirportSniper/",image:"https://cdn.spiele-kostenlos-online.de/wp-content/uploads/airport-sniper-01-160x110.webp"},
{title:"Traffic Racer 2",category:"racing",url:"https://cdn.htmlgames.com/TrafficRacer2/",image:"https://www.aktionspiele.de/uploaded/game/screenshot/trafficracer2800480.webp"},
{title:"Space Pinball",category:"racing",url:"https://cdn.htmlgames.com/SpacePinball/",image:"https://cdn.aptoide.com/imgs/1/b/1/1b1fa0c0dad30873323f0b001fc6e68e_icon.png"},
{title:"Higher or Lower",category:"racing",url:"https://cdn.htmlgames.com/HigherOrLower/",image:"https://www.denkspiele.com/uploaded/game/screenshot/higherorLower800480.webp"},
{title:"City Sniper",category:"action",url:"https://cdn.htmlgames.com/CitySniper/",image:"https://www.sellmyapp.com/wp-content/uploads/featured_image63417aad1a69e.png"},
{title:"Thief Puzzle",category:"action",url:"https://play.famobi.com/thief-puzzle",image:"https://via.placeholder.com/200"},
{title:"Geometry Dash",category:"racing",url:"https://gdbrowser.com",image:"https://via.placeholder.com/200"},
{title:"Galaxy Shooter",category:"action",url:"https://cdn.htmlgames.com/GalaxyShooter/",image:"https://via.placeholder.com/200"}

];

this.filtered=[...this.games];

this.init();
}

init(){
this.render(this.games);

document.getElementById("search").addEventListener("input",e=>{
const val=e.target.value.toLowerCase();
this.render(this.filtered.filter(g=>g.title.toLowerCase().includes(val)));
});
}

/* RENDER */
render(list){
const c=document.getElementById("games");
c.innerHTML="";
list.forEach(g=>{
const div=document.createElement("div");
div.className="game";
div.innerHTML=`<img src="${g.image}"><h3>${g.title}</h3>`;
div.onclick=()=>this.openGame(g.url);
c.appendChild(div);
});
}

/* FILTER */
filter(cat){
if(cat==="all"){
this.filtered=[...this.games];
} else {
this.filtered=this.games.filter(g=>g.category===cat);
}
this.render(this.filtered);
}

/* SORT */
sortAZ(){
this.filtered.sort((a,b)=>a.title.localeCompare(b.title));
this.render(this.filtered);
}

/* GAME */
openGame(url){
document.getElementById("gameWindow").style.display="block";
document.getElementById("player").src=url;
}

closeGame(){
document.getElementById("gameWindow").style.display="none";
}

}

const app=new App();

</script>

</body>
</html>
