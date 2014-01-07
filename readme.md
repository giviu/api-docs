# Giviu API docs

Esta es la documentacion de la API publica de Giviu.

## Contenido

Giviu expone una API rest bajo el siguiente URL:

    https://www.giviu.com/api

Todos los requests deben ser dirigidos hacia este endpoint.

## Parametros requeridos

Giviu expone una API publica, sin embargo, todas las solicitudes deben
llevar un parametro `client_id`. Este parametro es entregado a cada uno de
los socios y debe ser solicitado a `api@giviu.com`. Para los ejemplos de esta
documentacion, utilizaremos el client_id siguiente:

    client_id: 62b5bf5404

El client_id es *siempre* un string de 56 caracteres alfanumericos. Aunque en
estos ejemplos se usara uno de tan solo 10 caracteres.

## Recursos

### Obtener estado de una giftcard

    GET https://www.giviu.com/api/validate/giftcard/<GIFTCARD-CODE>

El codigo de giftcard es enviado al cliente y se compone de un string de
caracteres alfanumericos.

Ejemplo:

    GET https://www.giviu.com/api/validate/giftcard/e64422b2?client_id=62b5bf5404
