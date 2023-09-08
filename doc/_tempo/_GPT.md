

Voy a pasarte trozo de c�digos en vb.net, el codigo forma parte de un proyecto de Test en .NET que usa NUnit.
Ignora lo relacionado a la librer�a de NUnit y del testing y considera �nicamente la l�gica que est� testeando.
El codigo que te voy a dar testea las siguientes librer�as 

dinaup.client
dinaup.utilities


Son librer�as utilizadas para conectar al SaaS Dinaup.
Desde el api se puede
1. Consultar informes
2. Crear cuenta, iniciar sesi�n,cerrar sesi�n y recuperar contrase�a.
3. Acceder a datos de secciones
4. Editar, agregar, eliminar datos de secciones.
1. Consultar documentos din�micos 


La idea inicial es 

Se crea un DinaupClientC (dinaup.client.DinaupClientC) para conectar al API

    Public Client As dinaup.client.DinaupClientC
    Dim endPoint$ = "http://localhost:41100/"
    Dim publicKey$ = "c676603b-83db-4f5c-853b-efe255147360"
    Dim secretKey$ = "T@@yD=C@&wkfg=728gMyRATsco$ixf+XOK8{c+zjCytvt5GYT6%//*ZtV#vqgt?*"
    Dim defaultLocationId$ = "338226f9-5762-402d-a5df-c12103c798b9"
    Dim defaultUserId$ = "3c99edc3-e7a8-4f6b-8872-9804e3541553"
    Client = New DinaupClientC(endPoint, publicKey, secretKey, defaultLocationId, defaultUserId)
        
Se llama a DinaupClient_01.Ini() para iniciar la conexion 
se comprueba que est� ok If DinaupClient_01.Status = DinaupClientC.ClientStatus.Open Then 



Para entender un poco el resto de la librer�a 

1. En dinaup las secciones son literalmente tablas en la base de datos.
1. Los informes son Querys (osea selectes) que son consultas a dichas tablas, ej:  tales registros de tales secciones filtrados con tal criterio.


Digamos que, las secciones se utilizan para almacenar la informaci�n y los informes se usan para manipularla y obtenerlas.

Obtener informes tiene sus limites, pues estos son lista de datos con las limitaciones que tiene  postgre

Entonces, si lo que deseamos es utilizar los datos de una secci�n para crear documentos de texto plano complejos: json avanzados, html, xml....

Entonces Dinaup tiene una cosa que se llaman documentos din�micos.

Puedes imaginar documentos din�micos como PHP pero en lugar de PHP usa DinaScripts, dinascripts tiene una serie de funcioens y funcionalidades que no son importantes ahora.
Pero estas funciones permiten consultar datos desde cualquier seccion, connsultar datos de informes y operar toda esta informaci�n para obtener documentos complejos de texto plano,



