<!DOCTYPE html>
<html>
<head>
  <meta charset='utf-8' />
  <title>Digital Twins in Europe</title>
  <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
  <!-- Replace your_access_token with your Mapbox access token -->
  <script src='https://api.mapbox.com/mapbox-gl-js/v2.9.1/mapbox-gl.js'></script>
  <link href='https://api.mapbox.com/mapbox-gl-js/v2.9.1/mapbox-gl.css' rel='stylesheet' />
  <style>
    body { margin:0; padding:0; }
    #map { position:absolute; top:0; bottom:0; width:100%; }
    .mapboxgl-popup {
    max-width: 80%;
    color: #371d6d;
    font: 8px/12px 'Helvetica Neue', Arial, Helvetica, sans-serif;
    }
    


    /* Style the menu bar */
    /* Reset default styles */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* Set body font and background color */
body {
  font-family: sans-serif;
  background-color: #000;
  color: #fff;
}

/* Create a responsive grid layout */
.grid {
  display: flex;
  flex-wrap: wrap;
}

.grid > * {
  width: 100%;
}

@media (min-width: 600px) {
  .grid > * {
    width: 50%;
  }
}

@media (min-width: 900px) {
  .grid > * {
    width: 33.3333%;
  }
}

/* Style the header and navigation */
header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 20px;
}

header h1 {
  margin: 0;
  font-size: 2em;
  text-transform: uppercase;
  letter-spacing: 2px;
}


nav ul {
  display: flex;
  list-style: none;
}

nav li {
  margin: 0 10px;
}

nav a {
  color: #fff;
  text-decoration: none;
  font-weight: bold;
  text-transform: uppercase;
  letter-spacing: 1px;
  transition: color 0.2s;
}

nav a:hover {
  color: #0af;
}

/* Style the main content */
main {
  padding: 20px;
}

/* Style the footer */
footer {
  display: flex;
  bottom: 0;
  align-items: center;
  justify-content: space-between;
  background-color: #111;
  color: #fff;
  padding: 20px;
}

/* Add hover effects to buttons */
button {
  background-color: #0af;
  border: none;
  color: #fff;
  cursor: pointer;
  padding: 10px 20px;
  font-size: 1em;
  transition: background-color 0.2s;
}

button:hover {
  background-color: #00f;
}

/* Add responsive design styles */
@media (max-width: 600px) {
  nav ul {
    flex-direction: column;
  }

  nav li {
    margin: 10px 0;
  }
}

section {
  padding-top: 20px;
  padding-bottom: 40px;
}

header img {
  width: 200px;
  float: left;
  margin-right: 10px;
}

#map {
    width: 100%; /* Make the map fill the container */
    height: 100%;
    top: 80px;
    bottom: 50px;
}



  </style>
</head>
<body>
    <header>
        <!-- img src="logo.png" alt="Urban Digital Twin Observatory Logo"> -->
          <h1>Digital Twins in Europe</h1>
          <nav>
            <ul>
              <!--<li><a href="index.html#about">About</a></li> -->
              <!--<li><a href="index.html">Globe</a></li> -->
            </ul>
          </nav>
        </header>

        <main>
            <div id='map'></div>
              </div>
          </main>
          <footer>
            <!-- Add footer content here -->
            
          </footer>
        </body>
      </html>


 



  <script>

    // Initialize the map with your access token and any other options you want to set
    mapboxgl.accessToken = 'pk.eyJ1IjoiYnJ1bm9hdmlsYTUiLCJhIjoiY2tnZ21mYXczMDM1NzMzcW5nZ2F0Y2p5ciJ9.lcZsijSxzyUx2pNYIIUPQA';
    var map = new mapboxgl.Map({
      container: 'map', // container id
      style: 'mapbox://styles/brunoavila5/clvqiy96601oh01qrh1f1h0yb', // style URL
      center: [6, 50], // starting position [lng, lat]
      zoom: 3 // starting zoom
    });

    
    // Add zoom and rotation controls to the map.
    map.addControl(new mapboxgl.NavigationControl());


    map.on('style.load', () => {

map.setFog({
    color: 'rgb(186, 210, 235)', // Lower atmosphere  
    'high-color': 'rgb(36, 92, 223)', // Upper atmosphere
    'horizon-blend': 0.005, // Atmosphere thickness (default 0.2 at low zooms)
    'space-color': 'rgb(11, 11, 25)', // Background color
    'star-intensity': 0.3 // Background star brightness (default 0.35 at low zoooms )
});

});

    map.on('click', (event) => {
    // If the user clicked on one of your markers, get its information.
    const features = map.queryRenderedFeatures(event.point, {
      layers: ['symbols'] // replace with your layer name
    });
    if (!features.length) {
      return;
    }
    const feature = features[0];

   const popup = new mapboxgl.Popup({ offset: [0, -15] })
    .setLngLat(feature.geometry.coordinates)
    .setHTML(
      `<h3>${feature.properties.Initiative}</h3>
      <p>City/Region: ${feature.properties.City}</p>
      <p>Country: ${feature.properties.Country}</p>
      <p>Region: ${feature.properties.Region}</p>
      <p>Scale: ${feature.properties.Scale}</p>
      <p>Ownership: ${feature.properties.Ownership}</p>
      <p>Operator: ${feature.properties.Operator}</p>
      <p>Main Use Cases: ${feature.properties.MainUseCases}</p>
      <p><a href=${feature.properties.Reference} target="_blank">Reference</a></p>
      <p><a href=${feature.properties.Website} target="_blank">Direct Website (if existant)</a></p>`
    )  

    // If wanted, an image can be added in the poup e.g. src=${feature.properties.Image}
    // <img src='https://www.esri.com/content/dam/esrisites/en-us/digital-twin/assets/digital-twin-banner-foreground.png' width="250" height="150" alt="image">

        
    .addTo(map);

    });



  </script>
</body>
</html>
