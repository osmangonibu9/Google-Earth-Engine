# Google-Earth-Enginehttps://github.com/osmangonibu9/Google-Earth-Engine/blob/main/README.md
# AOI= Dhaka City shapefile
var no2 = ee.ImageCollection("COPERNICUS/S5P/OFFL/L3_NO2")

var image = no2.filterDate ('2024-01-01' , '2024-12-01')
              .select('NO2_column_number_density')
                .mean()
          .clip(AOI)

var band_viz = {
  min: 0,
  max: 0.0002,
  palette: ['black', 'blue', 'purple', 'cyan', 'green', 'yellow', 'red']
};
              
              
Map.addLayer(image,  band_viz)
Map.centerObject (AOI, 10)

// Export to Drive
Export.image.toDrive({
 image: image,
  description:'NO2 Concentration',
  scale: 30,
  region: AOI,
  maxPixels:1e13
})
