# SalinidadModelo
Promedio de salinidad mensual en la superficie del mar a partir de datos de Copernicus y visulaización en un geoportal
# Procesamiento de Salinidad Oceánica (Copernicus GLOBAL_MULTIYEAR_PHY_001_030)

## 📋 Métodos
1. **Datos fuente**:  
   - Producto: `GLOBAL_MULTIYEAR_PHY_001_030` (Copernicus Marine).  
   - Variables: Salinidad (`so`) diaria para mayo 2016.  
   - Área: -124°E a -80°E, 35°N a 10°S.  

2. **Procesamiento en R**:  
   - Cálculo del **promedio mensual** usando el paquete `terra`.  
   - Exportación a GeoTIFF (`salinidad.tif`).
if (!require("terra")) install.packages("terra")

# Cargar librerías
library(terra)

# 1. Leer el archivo NetCDF
ruta_nc <- "C:/Users/..."
datos_nc <- rast(ruta_nc, subds = "so")  # "so" = salinidad

# 2. Calcular el promedio mensual (media de los 31 días)
salinidad_promedio <- mean(datos_nc, na.rm = TRUE)

# 3. Guardar como GeoTIFF
ruta_geotiff <- "C:/Users/...tif"
writeRaster(salinidad_promedio, filename = ruta_geotiff, filetype = "GTiff", overwrite = TRUE)

# Mensaje de confirmación
print(paste("GeoTIFF guardado en:", ruta_geotiff))

#Resultado: [(https://github.com/GuillermoSan84/SalinidadModelo/blob/main/Salinidad.JPG?raw=true)
## 🛠️ Código
```r
library(terra)
datos <- rast("archivo.nc", subds = "so")
promedio <- mean(datos, na.rm = TRUE)
writeRaster(promedio, "salinidad.tif", filetype = "GTiff")
