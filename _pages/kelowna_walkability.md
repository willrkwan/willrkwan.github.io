---
title: "Analyzing Kelowna's Walkability"
permalink: /kelowna_walkability/
layout: single
author_profile: true
---

## Interactive Map (Sample Data)

<div id="map" style="height: 600px; border-radius: 12px; margin: 1em 0;"></div>

<!-- Leaflet CSS -->
<link rel="stylesheet" href="https://unpkg.com/leaflet/dist/leaflet.css" />

<!-- Leaflet JS -->
<script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>

<script>
  // Initialize map
  var map = L.map('map').setView([49.8879, -119.4960], 13); // Kelowna

  // Basemap
  var osm = L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '© OpenStreetMap contributors'
  }).addTo(map);

  // ===== Sample GeoJSON Layers =====
  // Final Walkability Index
  var walkability = L.geoJSON({
    "type": "FeatureCollection",
    "features": [
      {
        "type": "Feature",
        "properties": { "score": 75 },
        "geometry": {
          "type": "Polygon",
          "coordinates": [[
            [-119.5, 49.89],
            [-119.48, 49.89],
            [-119.48, 49.88],
            [-119.5, 49.88],
            [-119.5, 49.89]
          ]]
        }
      }
    ]
  }, {
    style: function (feature) {
      return {
        color: getColor(feature.properties.score),
        weight: 1,
        fillOpacity: 0.6
      };
    },
    onEachFeature: function (feature, layer) {
      layer.bindPopup("Walkability score: " + feature.properties.score);
    }
  });

  // Population Density
  var density = L.geoJSON({
    "type": "Feature",
    "properties": { "value": 3000 },
    "geometry": {
      "type": "Polygon",
      "coordinates": [[
        [-119.47, 49.89],
        [-119.45, 49.89],
        [-119.45, 49.87],
        [-119.47, 49.87],
        [-119.47, 49.89]
      ]]
    }
  }, {
    style: { color: "blue", weight: 1, fillOpacity: 0.4 },
    onEachFeature: function (feature, layer) {
      layer.bindPopup("Density: " + feature.properties.value + " people/km²");
    }
  });

  // Services (points)
  var services = L.geoJSON({
    "type": "FeatureCollection",
    "features": [
      {
        "type": "Feature",
        "properties": { "name": "Grocery Store A" },
        "geometry": { "type": "Point", "coordinates": [-119.49, 49.885] }
      },
      {
        "type": "Feature",
        "properties": { "name": "Bus Stop B" },
        "geometry": { "type": "Point", "coordinates": [-119.465, 49.88] }
      }
    ]
  }, {
    pointToLayer: function (feature, latlng) {
      return L.circleMarker(latlng, {
        radius: 6,
        fillColor: "purple",
        color: "#000",
        weight: 1,
        opacity: 1,
        fillOpacity: 0.8
      }).bindPopup("Service: " + feature.properties.name);
    }
  });

  // Slope
  var slope = L.geoJSON({
    "type": "Feature",
    "properties": { "value": 12 },
    "geometry": {
      "type": "Polygon",
      "coordinates": [[
        [-119.51, 49.89],
        [-119.505, 49.89],
        [-119.505, 49.885],
        [-119.51, 49.885],
        [-119.51, 49.89]
      ]]
    }
  }, {
    style: { color: "brown", weight: 1, fillOpacity: 0.4 },
    onEachFeature: function (feature, layer) {
      layer.bindPopup("Slope: " + feature.properties.value + "°");
    }
  });

  // ===== Layer Control =====
  var baseMaps = { "OpenStreetMap": osm };
  var overlayMaps = {
    "Final Walkability Index": walkability,
    "Population Density": density,
    "Services": services,
    "Slope": slope
  };
  L.control.layers(baseMaps, overlayMaps, { collapsed: false }).addTo(map);

  // Add default visible layers
  walkability.addTo(map);

  // ===== Legend for Walkability Index =====
  function getColor(score) {
    return score >= 80 ? '#006837' :
           score >= 60 ? '#31a354' :
           score >= 40 ? '#78c679' :
           score >= 20 ? '#c2e699' :
                         '#ffffcc';
  }

  var legend = L.control({position: 'bottomright'});
  legend.onAdd = function (map) {
    var div = L.DomUtil.create('div', 'info legend'),
        grades = [0, 20, 40, 60, 80];

    for (var i = 0; i < grades.length; i++) {
      div.innerHTML +=
        '<i style="background:' + getColor(grades[i] + 1) + 
        '; width: 18px; height: 18px; display: inline-block; margin-right: 5px;"></i> ' +
        grades[i] + (grades[i + 1] ? '&ndash;' + grades[i + 1] + '<br>' : '+');
    }
    return div;
  };
  legend.addTo(map);
</script>
