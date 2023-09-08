# Documentación: Conexión al SaaS Dinaup usando librerías dinaup.client y dinaup.utilities




## Introducción
Dinaup es un Software as a Service (SaaS) que permite gestionar información almacenada en tablas (denominadas "secciones") y consultar dicha información a través de consultas (denominadas "informes"). La finalidad de las librerías dinaup.client y dinaup.utilities es conectar al API de Dinaup, permitiendo así ejecutar distintas operaciones sobre las secciones y los informes.

## Conexión al API
Para establecer una conexión con el API de Dinaup:

Crear una instancia de dinaup.client.DinaupClientC.

```vb.net
Public Client As dinaup.client.DinaupClientC
Dim endPoint$ = "http://localhost:41100/"
Dim publicKey$ = "c676603b-83db-4f5c-853b-efe255147360"
Dim secretKey$ = "T@@yD=C@&wkfg=728gMyRATsco$ixf+XOK8{c+zjCytvt5GYT6%//*ZtV#vqgt?*"
Dim defaultLocationId$ = "338226f9-5762-402d-a5df-c12103c798b9"
Dim defaultUserId$ = "3c99edc3-e7a8-4f6b-8872-9804e3541553"
Client = New DinaupClientC(endPoint, publicKey, secretKey, defaultLocationId, defaultUserId)
```


Iniciar la conexión utilizando el método Ini().

``` vb.net
DinaupClient_01.Ini()
```
Verificar que la conexión haya sido establecida correctamente.

```vb.net

If DinaupClient_01.Status = DinaupClientC.ClientStatus.Open Then
   ' Conexión establecida
End If
```


## Conceptos Clave
- Secciones: Corresponden a tablas en la base de datos de Dinaup. Se utilizan para almacenar la información.
- Informes: Son consultas a las secciones, permitiendo filtrar y manipular datos. Funcionan como un "select" en SQL y tienen las limitaciones de PostgreSQL en cuanto a la lista de datos.
- Documentos Dinámicos: Permiten crear documentos de texto plano complejos como JSON, HTML, XML, entre otros. Estos documentos son generados usando DinaScripts, un lenguaje de scripting propio de Dinaup que ofrece diversas funciones y funcionalidades.
- Imagina los documentos dinámicos como si fueran scripts PHP, pero utilizando DinaScripts para manipular y consultar datos tanto de secciones como de informes.