# Conexión a Dinaup usando librerías dinaup.client  
 
La librería de Dinaup proporciona una interfaz para interactuar con el sistema Dinaup Tecnología, permitiendo gestionar datos, ejecutar consultas, generar documentos dinámicos y más. A continuación, se detalla cómo comenzar a usar esta librería.

## 📌 Conceptos Clave
- **Secciones**: Corresponden a tablas y campos en la base de datos de Dinaup. Se utilizan para almacenar la información. (Ej; Ventas, Compras, Productos..)
- **Registro**: Un dato en una sección. (un dato en una fila de una base de datos relacional.)
- **Informes**: Son consultas a las secciones, permitiendo filtrar y manipular datos, la información se obtiene en modo "filas". (Ej; Últimas 100 ventas, Libro diario, libro mayor...)
- **Documentos Dinámicos**: Permiten crear documentos de texto plano complejos como JSON, HTML, XML, entre otros. Estos documentos son generados usando DinaScripts, un lenguaje de scripting propio de Dinaup que ofrece diversas funciones y funcionalidades. Puedes imaginar documentos dinámicos como si fueran scripts PHP, pero utilizando DinaScripts para manipular y consultar datos tanto de secciones como de informes.
- **Archivos**: Se pueden adjuntar archivos a datos de secciones, por ejemplo, fotos de usuarios, pdfs. Son datos no estructuras que Dinaup guarda  en contenedores s3.
- **Anotaciones**: Comentarios ajuntos a registros, formación adicional no estructurada. 

## 📷  Capturas de pantalla
<details><summary>Ver captur de un dato</summary><img  src="https://cdn.dinaup.com/dinaup/recursos/capturas/25-acceso-rapido-entre-datos-blanco.png"></details>
<details><summary>Ver captura de un informe</summary><img  src="https://cdn.dinaup.com/dinaup/recursos/capturas/40-Total-seleccion-en-informes-blanco.png"></details>
<details><summary>Ver captura de una anotación</summary><img  src="https://cdn.dinaup.com/dinaup/recursos/capturas/15-archivos-adjuntos-blanco.png"></details>



---

# Librería .NET para Conectar con el API de Dinaup



## Importación del Espacio de Nombres
``` nuget
nuget install dinaup.client
nuget install dinaup.commonstructure
```

```
Imports dinaup.client
```
 


## 📡  Estableciendo la Conexión 

 
```vb
Public DinaupClient As dinaup.client.DinaupClientC
Dim endPoint = "******"
Dim publicKey = "******"
Dim secretKey = "******"
Dim defaultLocationId = "******"
Dim defaultUserId = "******"
Client = New DinaupClientC(endPoint, publicKey, secretKey, defaultLocationId, defaultUserId)
```


3. Iniciar la conexión:

``` vb
Await DinaupClient.IniAsync(360)  
If DinaupClient.Status = DinaupClientC.ClientStatus.Open Then
   ' Conexión establecida

   ' Se inicia con la sesión predeterminada.
    await DinaupClient.DefaultSessionUpdateAsync()

else
    
    ' Manejar error de conexión

End If
```
--- 



# 📊 Consultar Informes:

### Básica 
``` vb.net

Dim ModulosInstalados = New dinaup.commonstructure.Reports.FuncionalidadD.APIModulosInstaladosC()
Await ModulosInstalados.ExecuteQueryAsync(DinaupClient.DefaultSession, 1, 100)

For Each actual In ModulosInstalados.Rows
    Debug.Print(actual.TextoPrincipal)
Next

```

### Paginación

``` vb.net

Dim ModulosInstalados = New dinaup.commonstructure.Reports.FuncionalidadD.APIModulosInstaladosC()
Await ModulosInstalados.ExecuteQueryAsync(DinaupClient.DefaultSession, 1, 10)
Dim TotalPages = ModulosInstalados.TotalPages

Do
    For Each actual In ModulosInstalados.Rows
        '... procesamiento ...
    Next
Loop While ModulosInstalados.ExecuteQuery_NextPage

```


### Filtro
``` vb.net

Dim Versiones1y2ConOperadorIN = New dinaup.commonstructure.Reports.FuncionalidadD.APIModulosInstaladosC()
Versiones1y2ConOperadorIN.AddFilter("Version", "=", 1)
    Do
    For Each actual In ModulosInstalados.Rows
        '... procesamiento ...
    Next
Loop While ModulosInstalados.ExecuteQuery_NextPage

```

### Orden 

``` vb.net

Dim ModulosInstalados = New dinaup.commonstructure.Reports.FuncionalidadD.APIModulosInstaladosC()
ModulosInstalados.AddOrder("TextoPrincipal", False)
    Do
    For Each actual In ModulosInstalados.Rows
        '... procesamiento ...
    Next
Loop While ModulosInstalados.ExecuteQuery_NextPage

```
 
  

# 🔧 Operaciones con Datos


## Listar sección
El cliente de Dinaup está extremadamente optimizado para `consultar informes`. La opción de `listar datos` permite acceder a los datos de una sección sin necesidad de informes. Esto pude resultar conveniente para casos excepcionales ya que permite obtener todos los datos de una sección sin depender de un informe, pero esta funcionalidad consume hasta x20 lo que consume un informe además de no tener funcionalidades avanzadas como ordenar y paginación.


``` vb.net
Dim rowsRequestParameters As New RowsRequestParameters({"eliminado", "=", "0"})
rowsRequestParameters.Skip = 2
rowsRequestParameters.Limit = 18
Dim ModulosNoEliminados = Await dinaup.commonstructure.SectionsD.ModulosD.GetRowsAsync(DinaupClient, rowsRequestParameters)
```



## Operaciones de Escritura
Tanto agregar como editar.

### Individual

``` vb.net
Dim dataInsert = New Dictionary(Of String, String)
dataInsert.Add(SeccionDePruebasJSONES.TextoPrincipal, Date.UtcNow.ToSQL & " - " & Guid.NewGuid.ToString)
dataInsert.Add(SeccionDePruebasJSONES.ValorEntero, 2)
dataInsert.Add(SeccionDePruebasJSONES.CampoDecimal, 3)
Dim registroAModificarId = "" ' si es "" se agrega. Si es un guid se modifica
Dim writeOperationagregar = New dinaup.client.WriteOperation(id:=registroAModificarId, dataInsert)
Await DinaupClient.RunWriteOperationAsync(DinaupClient.DefaultSession, SeccionDePruebasJSONES._SectionID, writeOperationagregar, False)
```
### Por lotes 

``` vb.net
Dim listaDeOperaciones As New List(Of dinaup.client.WriteOperation)

', aquie puede agregar varios 
'listaDeOperaciones.Add()
'listaDeOperaciones.Add()
'listaDeOperaciones.Add()

',  ¡¡¡¡OJO!!! Todo  el bloque ¡¡¡¡DEBE TENER LAS MISMAS!!  COLUMNAS y pertenecer a la misma sección. 
Await DinaupClient.RunWriteOperationAsync(DinaupClient.DefaultSession, SeccionDePruebasJSONES._SectionID, listaDeOperaciones, False)
```

 


## Documento dinámmico

``` vb.net
Dim docdinamico = New dinaup.commonstructure.DynamicDocuments.APID.DocumentodePruebaAPIC("Hola")
docdinamico.ExecuteAsync(x.DefaultSession).Wait()
Dim responseJson = docdinamico.Response.DeserializarJSON(True)
Dim respuesta = responseJson.RootElement.ReadProperty("filas").Item(0).ReadSTR("respuesta")
```



## Alto rendimiento
En la documentación de la libreía [dinaup.client.highperfomance](dinaup.client.highperfomance.md), podras ver las opciones para almacenar caché en memoria de manera actualziada y crear colas para agregar los datos de manera asíncrona por lotes.








# 🗺 RoadMap

## Cliente
- [x] Cliente


## Sistema de sesiones
- [x] Registro de usuarios con validación por email
- [x] Inicio de sesión 
- [x] Recuperar contraseña
- [ ] SSO
- [ ] Doble factor


## Secciones 
- [x] Listar
- [x] Leer
- [x] Editar
- [x] Agregar
- [x] Eliminar
- [x] Anotaciones Comentarios
- [x] Anotaciones Archivos
- [x] Anotaciones Galería pública
- [ ] Restaurar
  

## Informes
- [x] Consultar
- [x] Filtrar
- [x] Ordenar
- [x] Paginación
- [x] Variables
- [ ] Agrupar

  

## Documentos dinámicos
- [x] Consultar
- [x] Variables

## Archivos 
- [x] Subir
- [x] Descargar
- [x] URLs firmadas
  

## Ejemplos 

