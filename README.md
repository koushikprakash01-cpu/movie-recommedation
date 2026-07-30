# movie-recommedation
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Movie Recommendation System</title>

<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;500;700&display=swap" rel="stylesheet">

<style>

*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:Poppins,sans-serif;
}

body{
background:#111;
color:white;
}

header{
background:#E50914;
padding:25px;
text-align:center;
}

header h1{
font-size:50px;
}

header p{
font-size:18px;
}

.search{
text-align:center;
margin:30px;
}

.search input{

width:60%;
padding:15px;
font-size:18px;
border:none;
border-radius:10px;

}

button{

padding:15px 25px;
background:red;
color:white;
border:none;
border-radius:10px;
cursor:pointer;
font-size:18px;

}

button:hover{

background:#ff3131;

}

section{

padding:40px;

}

h2{

margin-bottom:20px;
color:#ffcc00;

}

.genre-buttons button{

margin:8px;

}

.container{

display:grid;
grid-template-columns:repeat(auto-fit,minmax(250px,1fr));
gap:20px;

}

.card{

background:#222;
border-radius:15px;
overflow:hidden;
transition:.3s;

}

.card:hover{

transform:scale(1.05);

}

.card img{

width:100%;
height:320px;
object-fit:cover;

}

.card h3{

padding:10px;

}

.card p{

padding:0 10px 15px;

}

.rating{

color:gold;
font-weight:bold;

}

.preferences{

display:flex;
flex-wrap:wrap;
gap:15px;

}

label{

font-size:18px;

}

footer{

background:#222;
text-align:center;
padding:20px;
margin-top:50px;

}

</style>

</head>

<body>

<header>

<h1>🎬 Movie Recommendation System</h1>

<p>Discover Movies & Series Based On Your Taste</p>

</header>

<div class="search">

<input type="text" id="search" placeholder="Search Movie or Series">

<button onclick="searchMovie()">Search</button>

</div>

<section>

<h2>Browse by Genre</h2>

<div class="genre-buttons">

<button onclick="filterGenre('All')">All</button>

<button onclick="filterGenre('Action')">Action</button>

<button onclick="filterGenre('Comedy')">Comedy</button>

<button onclick="filterGenre('Drama')">Drama</button>

<button onclick="filterGenre('Sci-Fi')">Sci-Fi</button>

<button onclick="filterGenre('Romance')">Romance</button>

<button onclick="filterGenre('Horror')">Horror</button>

</div>

</section>

<section>

<h2>Choose Your Favorite Genres</h2>

<div class="preferences">

<label><input type="checkbox" value="Action"> Action</label>

<label><input type="checkbox" value="Comedy"> Comedy</label>

<label><input type="checkbox" value="Drama"> Drama</label>

<label><input type="checkbox" value="Sci-Fi"> Sci-Fi</label>

<label><input type="checkbox" value="Romance"> Romance</label>

<label><input type="checkbox" value="Horror"> Horror</label>

</div>

<br>

<button onclick="recommend()">Get Recommendations</button>

</section>

<section>

<h2>Movies & Series</h2>

<div class="container" id="movies"></div>

</section>

<section>

<h2>Recommended For You</h2>

<div class="container" id="recommendation"></div>

</section>

<footer>

Movie Recommendation System © 2026

</footer>

<script>

const movies=[

{
name:"Interstellar",
genre:"Sci-Fi",
rating:"⭐ 8.7",
type:"Movie",
image:"https://image.tmdb.org/t/p/w500/gEU2QniE6E77NI6lCU6MxlNBvIx.jpg"
},

{
name:"Inception",
genre:"Sci-Fi",
rating:"⭐ 8.8",
type:"Movie",
image:"https://image.tmdb.org/t/p/w500/9gk7adHYeDvHkCSEqAvQNLV5Uge.jpg"
},

{
name:"Avengers Endgame",
genre:"Action",
rating:"⭐ 8.4",
type:"Movie",
image:"https://image.tmdb.org/t/p/w500/or06FN3Dka5tukK1e9sl16pB3iy.jpg"
},

{
name:"Breaking Bad",
genre:"Drama",
rating:"⭐ 9.5",
type:"Series",
image:"https://image.tmdb.org/t/p/w500/ggFHVNu6YYI5L9pCfOacjizRGt.jpg"
},

{
name:"Money Heist",
genre:"Action",
rating:"⭐ 8.2",
type:"Series",
image:"https://image.tmdb.org/t/p/w500/mo0FP1GxOFZT4UDde7RFDz5APXF.jpg"
},

{
name:"Friends",
genre:"Comedy",
rating:"⭐ 8.9",
type:"Series",
image:"https://image.tmdb.org/t/p/w500/f496cm9enuEsZkSPzCwnTESEK5s.jpg"
},

{
name:"Titanic",
genre:"Romance",
rating:"⭐ 7.9",
type:"Movie",
image:"https://image.tmdb.org/t/p/w500/9xjZS2rlVxm8SFx8kPC3aIGCOYQ.jpg"
},

{
name:"The Conjuring",
genre:"Horror",
rating:"⭐ 7.5",
type:"Movie",
image:"https://image.tmdb.org/t/p/w500/wVYREutTvI2tmxr6ujrHT704wGF.jpg"
}

];

function display(data){

let output="";

data.forEach(movie=>{

output+=`

<div class="card">

<img src="${movie.image}">

<h3>${movie.name}</h3>

<p>${movie.type}</p>

<p>${movie.genre}</p>

<p class="rating">${movie.rating}</p>

</div>

`;

});

document.getElementById("movies").innerHTML=output;

}

display(movies);

function searchMovie(){

let value=document.getElementById("search").value.toLowerCase();

let result=movies.filter(movie=>movie.name.toLowerCase().includes(value));

display(result);

}

function filterGenre(genre){

if(genre=="All"){

display(movies);

return;

}

let result=movies.filter(movie=>movie.genre==genre);

display(result);

}

function recommend(){

let checked=[...document.querySelectorAll("input:checked")].map(c=>c.value);

let result=movies.filter(movie=>checked.includes(movie.genre));

let output="";

result.forEach(movie=>{

output+=`

<div class="card">

<img src="${movie.image}">

<h3>${movie.name}</h3>

<p>${movie.genre}</p>

<p>${movie.rating}</p>

</div>

`;

});

document.getElementById("recommendation").innerHTML=output;

}

</script>

</body>
</html>
