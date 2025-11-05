# Azure Storage

La API de Azure Storage permite subir todo tipo de archivos a la nube de forma segura y eficiente.

## Requisitos previos

Antes de utilizar la API, es necesario:

- Solicitar el espacio correspondiente en Azure.
- Solicitar un GUID de sistema con Daniel.

## Proceso de Solicitud

1. **Solicitud del Formato**  
   - **Responsable:** Ricardo Torres  
   - **Acción:** Enviar un correo electrónico a Ricardo solicitando el formato necesario.  
   - **Asunto del correo:** `Solicitud de cuenta de almacenamiento de Azure`  
   - **Copia:** Incluir en copia a Luis Ángel y Omar.

2. **Recepción y Llenado del Formato**  
   - **Responsable:** Solicitante  
   - **Acción:** Una vez recibido el formato, completarlo con la información requerida.  
   - **Copia:** Responder al correo original con el formato lleno, incluyendo a los mismos destinatarios (Ricardo, Luis Ángel y Omar).

3. **Creación de la Cuenta**  
   - **Responsable:** Ricardo Torres  
   - **Acción:** Crear la cuenta de almacenamiento en Azure.  
   - **Notificación:** Informar al solicitante que la cuenta ha sido creada mediante el mismo hilo de correo.  
   - **Copia:** Incluir en copia a Daniel Hernández.

4. **Entrega de Llaves GUID**  
   - **Responsable:** Daniel  
   - **Acción:** Responder al correo confirmando la creación de la cuenta.  
   - **Llaves:** Proveer dos llaves GUID: una para el entorno de producción y otra para el entorno de pruebas.

## Ficha tecnica 

POST
GetFile
http://10.0.5.73/Api/AzureStorage/beta}/AzureStorage/GetFile

GetFile API
This API endpoint retrieves a file from Azure Storage.
Request
Method: GET
URL: http://10.0.5.73/Api/AzureStorage/beta/AzureStorage/GetFile
Headers: Not specified
The request body should include the following parameters:
idDoc: 4346353 (This field it's the Document ID that want to get)
siteGuid: "98475FDD-6C87-319B-E054-E0071B2005F2" (This field it's the credential for the container)


Response
The response for this request is a JSON object with the following schema:


JSON








{
  "fileArray": "",
  "fileName": "",
  "fileUrl": "",
  "metadata": null,
  "extension": "",
  "idDocumento": 0,
  "codUser": null,
  "lista": "",
  "fullFilePath": null,
  "filePath": "",
  "urlSas": "",
  "fecExp": "",
  "rutaRaiz": "",
  "guid": "",
  "site": "",
  "appName": "",
  "appKey": null,
  "relativePath": ""
}




Body
{
  "idDoc": 22401136,//This field it's the Document ID that want to get
  "siteGuid": "F2761D10-0F97-4D2A-A3E5-7367745B5A0C"//This field it's the credential for the container
}

Ejemplo 
var options = new RestClientOptions("{{BetaAzureStorage}}/AzureStorage/GetFile")
{
  MaxTimeout = -1,
};
var client = new RestClient(options);
var request = new RestRequest("", Method.Get);
RestResponse response = await client.ExecuteAsync(request);
Console.WriteLine(response.Content);

POST
GetFileExists

{{BETA}}/AzureStorage/GetFileExists

Get File Exists
This endpoint makes an HTTP GET request to check if a file exists in the Azure Storage.
Request
The request body should be sent in raw format and include the following parameters:
name (string): This item must be empty.
fileArrayBase64 (string): This item must be empty.
list (string): This item must be empty.
path (string): This item must be empty.
idDoc (number): The document ID.
siteGuid (string): The unique identifier for the container.

Response
The response of this request is a JSON schema with a status code of 200 and content type of application/json. The response body will be a boolean value indicating whether the file exists or not.


JSON








{
  "type": "boolean",
  "description": "Indicates if the file exists in the Azure Storage."
}



Body
{
  "idDoc": 19258501,
  "siteGuid": "98475FDD-6C87-319B-E054-E0071B2005F2"
}

Ejemplo
var options = new RestClientOptions("{{BetaAzureStorage}}/AzureStorage/GetFileExists")
{
  MaxTimeout = -1,
};
var client = new RestClient(options);
var request = new RestRequest("", Method.Get);
RestResponse response = await client.ExecuteAsync(request);
Console.WriteLine(response.Content);

POST GetSiteByGuid
http://10.0.5.73/Api/AzureStorage/beta/AzureStorage/GetSiteByGuid

Get Site by GUID
This endpoint retrieves site information based on the specified site GUID.
Request
Method: GET
URL: {{BetaAzureStorage}}/AzureStorage/GetSiteByGuid
Headers:
Content-Type: application/json

Body:
idDoc: (0)
siteGuid: (string) - Specifies the site GUID for the desired site.


Response
The response for this request is a JSON object with the following schema:


JSON








{
  "guid": "",
  "site": "",
  "appName": "",
  "appKey": "",
  "relativePath": ""
}


guid: (string) - The GUID of the site.
site: (string) - The site information.
appName: (string) - The name of the application.
appKey: (string) - The application key.
relativePath: (string) - The relative path.

Example Response


JSON








{
    "guid": "1840731D-0C74-499E-8F3A-E0CB4F76668B",
    "site": "fapspruebablob",
    "appName": "pocstorageaccount",
    "appKey": "uhp9Q7bSFsbJyNhmNgQ2aE5wMb8VvUnBLE0BAhahNDHDLmqmM+H78S0+XxooNDygcCmzO9YbYP+AStcA9V1w==",
    "relativePath": "fapspruebablob"
}


body
{
  //"idDoc": 0,//This field must be empty.
  "siteGuid": "1840731D-0C74-499E-8F3A-E0CB4F76668B"//This field specifies the site you want.
}

var options = new RestClientOptions("{{BETA}}/AzureStorage/GetSiteByGuid")
{
  MaxTimeout = -1,
};
var client = new RestClient(options);
var request = new RestRequest("", Method.Get);
RestResponse response = await client.ExecuteAsync(request);
Console.WriteLine(response.Content);

POST
SaveFileCustomList
https://localhost:44321/AzureStorage/SaveFileCustomList


Save File Custom List
This endpoint allows you to save a file to a custom list in Azure Storage.
Request Body
idDoc (number): This field must have a value of 0.
siteGuid (string): Indicates where the document will be saved.
name (string): Indicates the name of the file.
fileArrayBase64 (string): The file encoded in base64 string.
list (string): Indicates the master folder of the tree path.

Response
The response is a JSON schema with a status code of 200 and a content type of application/json.


JSON








{
  "type": "number"
}



Body
{
  "idDoc": 0,//This field must have a 0
  "siteGuid": "1840731D-0C74-499E-8F3A-E0CB4F76668B",//This field indicate where is going to be saved the document
  "name": "Subcarpeta/ejemplo_user_con_Usuario.txt",//This field indicate the name of the file,
  "fileArrayBase64": "SG9sYSBtdW5kbw==",//This field it's the file in stringbase64
  "list": "PruebaPOSTMAN",//This field indicate the master folder of the tree path
  "codUser": "LLARA"
}

var options = new RestClientOptions("{{BetaAzureStorage}}/AzureStorage/SaveFileCustomList")
{
  MaxTimeout = -1,
};
var client = new RestClient(options);
var request = new RestRequest("", Method.Post);
var body = @"{
" + "\n" +
@"  ""idDoc"": 0,//This field must have a 0
" + "\n" +
@"  ""path"": """",//This field must be empty
" + "\n" +
@"  ""siteGuid"": ""1840731D-0C74-499E-8F3A-E0CB4F76668B"",//This fiel indicate where is going to be saved the document
" + "\n" +
@"  ""name"": ""Subcarpeta/ejemplo.png"",//This field indicate the name of the file
" + "\n" +
@"  ""fileArrayBase64"": ""iVBORw0KGgoAAAANSUhEUgAAArwAAACvCAYAAAAfZw1fAAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAuvhJREFUeNrsvQmQHdd1333eMjsGswAYbARAguAmcZFEkbK4yIrMfEpEVUmK5JRli84X2Y"",//This field it's the file in stringbase64
" + "\n" +
@"  ""list"": ""PruebaPOSTMAN/""//This field indicate the master folder of the tree path
" + "\n" +
@"}";
request.AddParameter("text/plain", body,  ParameterType.RequestBody);
RestResponse response = await client.ExecuteAsync(request);
Console.WriteLine(response.Content);

reponse 
19346280
POST
SaveFileDefaultList
https://localhost:44321/AzureStorage/SaveFileDefaultList

SaveFileDefaultList
This endpoint allows you to save a file to the Azure Storage with default settings.
Request Body
idDoc (number): Must be set to 0.
path (string): Must be empty.
siteGuid (string): Indicates where the document will be saved.
name (string): Indicates the name of the file.
fileArrayBase64 (string): The file content in base64 string format.
list (string): Must be empty.

Response
The response is a JSON schema with the following structure:


JSON








{
  "type": "number"
}




body

{
  "idDoc": 0,//This field must have a 0
  "siteGuid": "1840731D-0C74-499E-8F3A-E0CB4F76668B",//This fiel indicate where is going to be saved the document
  "name": "Subcarpeta/ejemplo_usuario.txt",//This field indicate the name of the file
  "fileArrayBase64": "SG9sYSBtdW5kbw=="//This field it's the file in stringbase64
}

reponse 
19346280

POST
SaveFileB64
https://localhost:44321/AzureStorage/SaveFileB64

SaveFileB64
This endpoint allows you to save a file to the Azure Storage with the provided payload in base64 format.
Request Body
Guid (string): A unique identifier for the file.
RutaArchivo (string): The path where the file will be saved.
NombreArchivo (string): The name of the file.
StringArchivo (string): The file content in base64 string format.

Response
The response is a JSON schema with the following structure:


JSON








{
  "type": "number"
}



body
{
    "Guid": "1840731D-0C74-499E-8F3A-E0CB4F76668B",//Este campo indica el Guid asignado por cuenta de almacenamiento/Environment
    "RutaArchivo": "PruebaAPI/Subcarpeta",//Este campo guarda la ruta que precede al archivo, no se toman en cuenta diagonales finales ni al principio
    "NombreArchivo": "textoPrueba_WCODUSER.txt",//debe indicarse con todo y su extension
    "StringArchivo": "SGVsbG8gV29ybGQ=",//String en base 64
    "CodUser": "LLARA"//String que indica que usuario subio el archivo, es opcional
}

POST
SaveFileBytes
POST
{{BETA}}/AzureStorage/SaveFileBytes

SaveFileB64
This endpoint allows you to save a file to the Azure Storage with the provided payload in base64 format.
Request Body
Guid (string): A unique identifier for the file.
RutaArchivo (string): The path where the file will be saved.
NombreArchivo (string): The name of the file.
BytesArchivo (byte[]): The file content in byte array format.

Response
The response is a JSON schema with the following structure:


JSON








{
  "type": "number"
}



{
    "Guid": "1840731D-0C74-499E-8F3A-E0CB4F76668B",//Este campo indica el Guid asignado por cuenta de almacenamiento/Environment
    "RutaArchivo": "PruebaAPI/Subcarpeta",//Este campo guarda la ruta que precede al archivo, no se toman en cuenta diagonales finales ni al principio
    "NombreArchivo": "textoPrueba.txt",//debe indicarse con todo y su extension
    "BytesArchivo": "SGVsbG8gV29ybGQ="//Arreglo de bytes [], en POSTMAN se tiene que mandar como un Base 64 pero a nivel codigo se manda un byte[] 
}

POST
GetFileBytes
{{BETA}}/AzureStorage/GetFileBytes
AzureStorage GetFileBytes
This endpoint allows you to retrieve file bytes from Azure Storage.
Request Body
IdDoc (integer): The ID of the document to retrieve.
SiteGuid (string): The unique identifier of the site.

Response
Status: 200
Content-Type: application/json
body
{
    "IdDoc": 19598786,//This field is the file identifier
    "SiteGuid": "1840731D-0C74-499E-8F3A-E0CB4F76668B"//This field verify the origin of the request
}

POST
GetUrlSAS
{{BETA}}/AzureStorage/GetFileURLSas

The POST request to /AzureStorage/GetFileURLSas endpoint is used to retrieve a URL with a Shared Access Signature (SAS) for a specific file in Azure Storage.
Request Body
IdDoc (number) - The ID of the document.
SiteGuid (string) - The unique identifier for the site.

Response
The response is a JSON object containing the URL with a Shared Access Signature (SAS) for the requested file in the Azure Storage. Since the user wants the response documented as a JSON schema, the response schema can be defined as follows:


JSON








{
    "type": "object",
    "properties": {
        "url": {
            "type": "string",
            "description": "The URL with a Shared Access Signature (SAS) for the requested file."
        }
    }
}



body

{
    "IdDoc": 19346280,//This field is the file identifier
    "SiteGuid": "1840731D-0C74-499E-8F3A-E0CB4F76668B"//This field verify the origin of the request
}



