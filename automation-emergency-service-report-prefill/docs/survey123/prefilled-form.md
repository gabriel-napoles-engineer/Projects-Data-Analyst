# Survey123 Prefilled Form

Este documento describe cómo se genera el enlace prellenado utilizado para los reportes de servicios de emergencia en **ArcGIS Survey123**.

## Objetivo

El prellenado permite cargar automáticamente información del incidente antes de que el personal operativo abra el formulario.

De esta manera, se evita capturar manualmente datos que ya fueron obtenidos desde **Active911** y el **estado de fuerza**.

## Estructura del enlace

Survey123 permite asignar valores a campos específicos mediante parámetros incluidos en la URL.

Ejemplo:

```text
https://survey123.arcgis.com/share/XXXX?field:correo_electr_nico=example@gmail.com&field:folio_active_911=000010
```

La estructura general es:

```text
https://survey123.arcgis.com/share/FORM_ID?field:FIELD_NAME=VALUE
```

Para agregar más campos se utiliza `&`:

```text
?field:campo1=valor1&field:campo2=valor2&field:campo3=valor3
```

## Datos utilizados

El enlace se construye dinámicamente en Make utilizando información proveniente de dos fuentes principales.

### Active911

Datos extraídos del correo mediante el modelo de IA, por ejemplo:

* Correo
* Estación
* Folio Active911
* Folio CECOM
* Calle
* Colonia
* Incidente
* Giro
* Unidades

### Estado de Fuerza

Información obtenida del último registro disponible, como:

* Personal en turno
* Unidades activas
* Asignación de personal
* Estación

## Generación en Make

Los valores obtenidos durante el flujo se convierten en variables y posteriormente se insertan en la URL de Survey123.

Ejemplo simplificado:

```text
https://survey123.arcgis.com/share/XXXX
?field:folio_active_911={{active911}}
&field:calle={{calle}}
&field:colonia={{Colonia}}
&field:incidente={{Incidente}}
```

El enlace resultante se almacena junto con la información procesada y posteriormente se envía por correo electrónico a la estación correspondiente.

## Resultado

Cuando el personal abre el enlace, Survey123 carga automáticamente los campos disponibles con la información del servicio.

El usuario únicamente debe revisar los datos y completar la información que no puede ser generada automáticamente, principalmente la descripción de las actividades realizadas durante la atención de la emergencia.

## Consideraciones

Los nombres utilizados en `field:` deben corresponder exactamente con los nombres internos de los campos configurados en Survey123.

También es necesario codificar correctamente caracteres especiales, espacios y valores que puedan afectar la estructura de la URL.

