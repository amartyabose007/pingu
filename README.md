<!DOCTYPE html>
<html dir="ltr">
<head>
   <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
   <meta name="viewport" content="initial-scale=1, maximum-scale=1,user-scalable=no" />
   <title>Assignment@1093545</title>
   <link rel="stylesheet" href="https://js.arcgis.com/3.20/dijit/themes/claro/claro.css">
   <link rel="stylesheet" href="https://js.arcgis.com/3.20/esri/css/esri.css">
   <link rel="stylesheet" href="https://www.w3schools.com/w3css/4/w3.css">
   <style>
      html,
      body,
      #map {
         height: 100%;
         width: 100%;
         margin: 0;
         padding: 0;
      }
      #search {
         display: block;
         position: absolute;
         z-index: 2;
         top: 70px;
         left: 74px;
         
      }
      #LocateButton {
      position: absolute;
      top: 150px;
      left: 20px;
      z-index: 30;}
      
      #BasemapToggle {
      position: absolute;
      top: 120px;
      right: 20px;
      z-index: 50;}
      body{        
        padding-top: 60px;
        padding-bottom: 40px;
    }
    .fixed-header, .fixed-footer{
        width: 100%;
        position: fixed;        
        background: #FFFF00;
        padding: 15px 0;
        color: 	#FF0000;
    }
    .fixed-header{
        top: 0;
    }
    .fixed-footer{
        bottom: 0;
        
    }
    .container{
        width: 80%;
        margin: 0 auto; /* Center the DIV horizontally */
    }
    
     
   </style>

   
<script src="https://js.arcgis.com/3.20/"></script>
   <script>
      require([
        "esri/map", "esri/dijit/Search", "esri/layers/FeatureLayer", "esri/InfoTemplate", "esri/dijit/LocateButton","esri/dijit/BasemapToggle","esri/dijit/Scalebar",
        "dojo/parser","dijit/layout/BorderContainer", "dijit/layout/ContentPane","dojo/domReady!"
      ], function (Map, Search, FeatureLayer, InfoTemplate,LocateButton,BasemapToggle,Scalebar,
        parser) {
            parser.parse();
         var map = new Map("map", {
            basemap: "streets",
            center: [ 85.371119,17.280739], // lon, lat
            zoom: 4
         });

         var search = new Search({
            enableButtonMode: true, 
            enableLabel: false,
            enableInfoWindow: true,
            showInfoWindowOnSelect: false,
            map: map
         }, "search");

         var sources = search.get("sources");

      
         sources.push({
            featureLayer: new FeatureLayer("https://services.arcgis.com/V6ZHFr6zdgNZuVG0/arcgis/rest/services/CongressionalDistricts/FeatureServer/0"),
            searchFields: ["DISTRICTID"],
            displayField: "DISTRICTID",
            exactMatch: false,
            outFields: ["DISTRICTID", "NAME", "PARTY"],
            name: "Congressional Districts",
            placeholder: "3708",
            maxResults: 6,
            maxSuggestions: 6,

            
            infoTemplate: new InfoTemplate("Congressional District", "District ID: ${DISTRICTID}</br>Name: ${NAME}</br>Party Affiliation: ${PARTY}"),
            enableSuggestions: true,
            minCharacters: 0
         });

        
         
         search.set("sources", sources);

         search.startup();
         
         
          geoLocate = new LocateButton({
        map: map
      }, "LocateButton");
      geoLocate.startup();
      
      var toggle = new BasemapToggle({
        map: map,
        basemap: "hybrid"
      }, "BasemapToggle");
      toggle.startup();

       var scalebar = new Scalebar({
          map: map,
          // "dual" displays both miles and kilometers
          // "english" is the default, which displays miles
          // use "metric" for kilometers
          scalebarUnit: "dual"
        });

      });
   </script>
</head>

<body>
  <div class="fixed-header" ><center><h3>The Assignment</h3></center></div>
  <div class="fixed-footer" ><center>EMP#1093545</center></div>
   <div id="search"></div>
   <div id="LocateButton"></div>
    <div id="BasemapToggle"></div>
   <div id="map"></div>
   
</body>

</html>
