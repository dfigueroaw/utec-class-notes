Si el porcentaje de data no valida es menor a 5%, normalmente no habría problemas mayores eliminando la data no valida sin mayor problema (sin embargo, a veces es necesario hacer un análisis mas detallado). En caso sea mayor (o se vea conveniente) se suelen utilizar técnicas de imputación, que refieren a técnicas las cuales nos permiten reemplazar la data faltante y darle un valor con el que podamos realizar un análisis con normalidad.

Existen distintas técnicas de imputación para completar los datos faltantes (NA) de un dataframe...
**Numéricas**
- **Media**: Normalmente se toma esta cuando la media es representativa (Analizando el coeficiente de variación, normalmente se toma cuando es menor que 0.1, pero podemos tomar 0.3)
- **Mediana**: Tomamos cuando el coeficiente de variación es mayor que 0.3 pero menor que 0.6. Incluso si es mayor a 0.6, se toma la mediana.
**No numéricas**
- Moda

Un conjunto de datos sin moda se llama **amodal** (lo cual ocurre cuando todos los datos de nuestro conjunto de datos tienen la misma frecuencia). Por otro lado, cuando un conjunto de datos tiene múltiples modas se le llama multimodal.