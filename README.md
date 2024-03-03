// API URLs for fetching movie data
const APIURL = "https://api.themoviedb.org/3/discover/movie?sort_by=popularity.desc&api_key=04c35731a5ee918f014970082a0088b1&page=1";
const IMGPATH = "https://image.tmdb.org/t/p/w1280";
const SEARCHAPI = "https://api.themoviedb.org/3/search/movie?&api_key=04c35731a5ee918f014970082a0088b1&query=";

// HTML elements
const main = document.getElementById("main");
const form = document.getElementById("form");
const search = document.getElementById("search");

// Initially get popular movies
getMovies(APIURL);

// Async function to fetch and handle movie data
async function getMovies(url) {
  const resp = await fetch(url);
  const respData = await resp.json();

  // Log the fetched movie data
  console.log(respData);

  // Display the movies on the webpage
  showMovies(respData.results);
}

// Function to display movies on the webpage
function showMovies(movies) {
  // Clear the main container
  main.innerHTML = "";

  // Iterate through each movie and create HTML elements to display them
  movies.forEach((movie) => {
    const { poster_path, title, vote_average, overview } = movie;

    // Create a div element for each movie
    const movieEl = document.createElement("div");
    movieEl.classList.add("movie");

    // Populate the div with movie information
    movieEl.innerHTML = `
      <img src="${IMGPATH + poster_path}" alt="${title}"/>
      <div class="movie-info">
        <h3>${title}</h3>
        <span class="${getClassByRate(vote_average)}">${vote_average}</span>
      </div> 
      <div class="overview">
        <h2>Overview:</h2>
        ${overview}
      </div>
    `;

    // Append the movie element to the main container
    main.appendChild(movieEl);
  });
}

// Function to determine the CSS class based on the movie rating
function getClassByRate(vote) {
  if (vote >= 8) {
    return 'green';
  } else if (vote >= 5) {
    return 'orange';
  } else {
    return 'red';
  }
}

// Event listener for the form submission (search)
form.addEventListener("submit", (e) => {
  e.preventDefault();

  // Get the search term from the input field
  const searchTerm = search.value;

  // If a search term is provided, fetch and display the corresponding movies
  if (searchTerm) {
    getMovies(SEARCHAPI + searchTerm);
    search.value = "";
  }
});


END OF CODEEEEEE

Certainly! Let's break down the provided JavaScript code line by line:

javascript
Copy code
// API URLs for fetching movie data
const APIURL = "https://api.themoviedb.org/3/discover/movie?sort_by=popularity.desc&api_key=04c35731a5ee918f014970082a0088b1&page=1";
const IMGPATH = "https://image.tmdb.org/t/p/w1280";
const SEARCHAPI = "https://api.themoviedb.org/3/search/movie?&api_key=04c35731a5ee918f014970082a0088b1&query=";

// HTML elements
const main = document.getElementById("main");
const form = document.getElementById("form");
const search = document.getElementById("search");
These lines declare and initialize constants for the API URLs and HTML elements. The APIURL is for fetching popular movies, IMGPATH is the base URL for movie poster images, and SEARCHAPI is for searching movies by a user-provided query. The main, form, and search variables store references to HTML elements with corresponding IDs.
javascript
Copy code
// Initially get popular movies
getMovies(APIURL);
This line calls the getMovies function with the APIURL as an argument, fetching and displaying popular movies on the webpage when it loads.
javascript
Copy code
// Async function to fetch and handle movie data
async function getMovies(url) {
  const resp = await fetch(url);
  const respData = await resp.json();

  // Log the fetched movie data
  console.log(respData);

  // Display the movies on the webpage
  showMovies(respData.results);
}
This block defines an asynchronous function getMovies that takes a URL as an argument. It uses the fetch function to make a network request to the provided URL, then converts the response to JSON using resp.json(). The fetched movie data is logged to the console, and the showMovies function is called with the movie results.
javascript
Copy code
// Function to display movies on the webpage
function showMovies(movies) {
  // Clear the main container
  main.innerHTML = "";

  // Iterate through each movie and create HTML elements to display them
  movies.forEach((movie) => {
    const { poster_path, title, vote_average, overview } = movie;

    // Create a div element for each movie
    const movieEl = document.createElement("div");
    movieEl.classList.add("movie");

    // Populate the div with movie information
    movieEl.innerHTML = `
      <img src="${IMGPATH + poster_path}" alt="${title}"/>
      <div class="movie-info">
        <h3>${title}</h3>
        <span class="${getClassByRate(vote_average)}">${vote_average}</span>
      </div> 
      <div class="overview">
        <h2>Overview:</h2>
        ${overview}
      </div>
    `;

    // Append the movie element to the main container
    main.appendChild(movieEl);
  });
}
This block defines the showMovies function, which takes an array of movies as an argument. It first clears the content of the main container. Then, it iterates through each movie, creating a new div element for each. The movie information is added to the div using string interpolation, and the resulting HTML is appended to the main container.
javascript
Copy code
// Function to determine the CSS class based on the movie rating
function getClassByRate(vote) {
  if (vote >= 8) {
    return 'green';
  } else if (vote >= 5) {
    return 'orange';
  } else {
    return 'red';
  }
}
This block defines the getClassByRate function, which takes a movie rating as an argument and returns a CSS class name based on the rating. If the rating is 8 or higher, it returns 'green'; if it's between 5 and 8, it returns 'orange'; otherwise, it returns 'red'.
javascript
Copy code
// Event listener for the form submission (search)
form.addEventListener("submit", (e) => {
  e.preventDefault();

  // Get the search term from the input field
  const searchTerm = search.value;

  // If a search term is provided, fetch and display the corresponding movies
  if (searchTerm) {
    getMovies(SEARCHAPI + searchTerm);
    search.value = "";
  }
});
This block adds an event listener to the form for the "submit" event. When the form is submitted, it prevents the default form submission behavior (page reload). It then retrieves the search term from the input field, and if a search term is provided, it calls the getMovies function with the search API URL and the search term appended. Finally, it clears the search input field.



