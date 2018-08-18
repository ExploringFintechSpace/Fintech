<html>
     <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <style>
            html {
  font-family: "Avenir Next", Helevetica, sans-serif;
  text-align: center;}

body {margin: 0 auto;}

h1,h2 {font-weight: 300;}
        </style>
        <title> Weather </title>
        <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js"></script>
     </head>

     <body>


        <h1><div id="temp"></div></h1>
	<h2><div id="Summary"></div></h2>
	<h3><div id="icon"></div></h3>
<p id ="demo"></p>

<script>
var greeting;
if(icon="rain"){
greeting = "Its raining"
document.getElementById("demo").innerHTML = greeting;
}
</script>


        <h2><div id="location"></div></h2>
	<h3><div id="map"></div></h3>
	<h3><div id="remap"></div></h3>
        
</body>

     <script>
         function weather() {
  var location = document.getElementById("location");
  var map = document.getElementById("map");
  var remap = document.getElementById("remap");
  var apiKey2 = "8fb2a533f58f18d31e3aa1d2b98395f0";
  var url = "https://api.darksky.net/forecast/";

  navigator.geolocation.getCurrentPosition(success, error);

  function success(position) {
    latitude = position.coords.latitude;
    longitude = position.coords.longitude;

    location.innerHTML =
      "Latitude is " + latitude +" "+ "Longitude is " + longitude+ " ";


    $.getJSON(
      url + apiKey2 + "/" + latitude + "," + longitude + "?callback=?",
      function(data) {
        $("#temp").html(data.currently.temperature + " F");
        $("#Summary").html(data.daily.summary);
	$("#icon").html(data.daily.icon);

      }
);

var img_url = "https://maps.googleapis.com/maps/api/geocode/json?latlng=40.714224,-73.961452&key=AIzaSyDji7Xfq3-P-DQBnewbPRqZH0GojSHJhsI";

    $.getJSON(
      img_url + "?callback=?",
      function(data) {
        $("#remap").html(data.formatted_address);
        
      }
);

  }

  function error() {
    location.innerHTML = "Unable to retrieve your location";
  }



  location.innerHTML = "Locating...";
}
weather();
     </script>
 
 </html>
