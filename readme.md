# Giviu API docs

Esta es la documentación de la API pública de Giviu.

## Contenido

Giviu expone una API Http bajo el siguiente URL:

    https://www.giviu.com/api

Todos los requests deben ser dirigidos hacia este endpoint.

## Parametros requeridos

Giviu expone una API pública, sin embargo, todas las solicitudes deben
llevar un parámetro `client_id`. Este parámetro es entregado a cada uno de
los socios y debe ser solicitado a `api@giviu.com`. Para los ejemplos de esta
documentación, utilizaremos el client_id siguiente:

    client_id: 62b5bf5404

El client_id es *siempre* un string de 56 caracteres alfanumericos. Aunque en
estos ejemplos se usará uno de tan solo 10 caracteres.

## Recursos

### Obtener estado de una giftcard

    https://www.giviu.com/api/validate/giftcard/<GIFTCARD-CODE>

Metodo HTTP: GET

El código de giftcard es enviado al cliente y se compone de un string de
caracteres alfanumericos.

Ejemplo:

    GET https://www.giviu.com/api/validate/giftcard/e64422b2?client_id=62b5bf5404

Respuesta:

    // HTTP/1.0 200 OK
    // Content-Type: application/json
    {
        "giftcard": {
            "id": "e64422b2",
            "from": "email_original@dominio.com",
            "to": "email_recibidor@dominio.com",
            "giftcard_price": 30000
            "already_validated": true,
            "validation_date": "2014-01-07T22:21:36+00:00",
        }
    }


#### Otros resultados posibles

Giviu presenta una API Http y se ajusta a algunas de las definiciones de esta arquitectura, otros
resultados posibles son:

 * Bad Request (Http Status Code: 400): Solicitud erronea, no todos los parametros se
 encuentran en la solicitud, no hay un parametro client_id, etc.
 * Not Found (Http Status Code: 404): La giftcard solicitada no existe.

En esta versión inicial de la API, no se especifica que problema en particular es
el que genera un resultado. En ediciones posteriores esta información sera incluida
en formato JSON.

### Validar una giftcard

Para cambiar el estado de una giftcard a estado "validada" se debe utilizar el mismo
URL utilizado para obtener el estado de una giftcard:

    https://www.giviu.com/api/validate/giftcard/<GIFTCARD-CODE>

Metodo HTTP: PUT

El metodo PUT cambiara el estado de una giftcard hacia el estado *ya* validado, esto
es, debe cambiarse el estado de una giftcard cuando un cliente se presente con una
giftcard para ser cobrada.

Ejemplo:

    PUT https://www.giviu.com/api/validate/giftcard/e64422b2?client_id=62b5bf5404

Respuesta 1, se ha cambiado el estado de la giftcard exitosamente:

    // HTTP/1.0 200 OK
    // Content-Type: application/json
    {
        "status": "The giftcard has been validated"
    }

Respuesta 2, no se ha cambiado el estado de la giftcard:

    // HTTP/1.0 400 OK
    // Content-Type: application/json
    {
        "validation_date": "2014-01-07T22:21:36+00:00",
        "status": "The giftcard has already been validated"
    }
