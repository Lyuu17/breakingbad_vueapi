# Breaking Bad API

Utiliza la API de [breakingbadapi.com](https://github.com/timbiles/Breaking-Bad--API). Dejó de funcionar en Diciembre 2022.

## Preview

![image](https://user-images.githubusercontent.com/14199521/215203478-222e5da4-a958-4fb6-9b79-d224f64f050f.png)

## Descripción de la API
### URL base: https://www.breakingbadapi.com/api/


|Función|Endpoint|
|---|---|
Obtener todos los personajes junto a sus datos | /api/characters
Obtener un personaje por ID del personaje | /api/characters/[id]
Obtener personajes búsqueda de nombre | /api/characters?name=[nombre]

Ejemplo de personaje obtenido con /api/characters/1

```json
{
    char_id: 1,
    name: "Walter White",
    birthday: "09-07-1958",
    occupation: [
        "High School Chemistry Teacher",
        "Meth King Pin"
    ],
    img: "https://images.amcnetworks.com/amc.com/wp-content/uploads/2015/04/
    cast_bb_700x1000_walter - white - lg.jpg ",
    status: "Deceased",
    appearance: [1, 2, 3, 4, 5],
    nickname: "Heisenberg",
    portrayed: "Bryan Cranston"
}
```

Ejemplo de lista de personajes obtenidos buscando por Walter White: /api/characters?name=Walter+White

```json
{
  char_id: 1,
  name: "Walter White",
  birthday: "09-07-1958",
  occupation: [
    "High School Chemistry Teacher",
    "Meth King Pin"
  ],
  img: "https://images.amcnetworks.com/amc.com/wp-content/uploa...",
  status: "Deceased",
  appearance: [1, 2, 3, 4, 5],
  nickname: "Heisenberg",
  portrayed: "Bryan Cranston",
  better_call_saul_appearance: [ ]
},
{
  char_id: 4,
  name: "Walter White Jr.",
  birthday: "07-08-1993",
  occupation: [
    "Teenager"
  ],
  img: "https://media1.popsugar-assets.com/files/thumbor/WeLUSvbA...",
  status: "Alive",
  nickname: "Flynn",
  appearance: [ 1, 2, 3, 4, 5 ],
  portrayed: "RJ Mitte",
  category: "Breaking Bad",
  better_call_saul_appearance: [ ]
}
```

## Componentes
### BotonVerInfo.vue
- Props
  - id { type: Number, required }
### Buscar.vue
- Props
  - buscando { type: Boolean, required }
  - mostrar_fav { type: Boolean, required }
### Datos.vue
- Props
  - datos { type: Array, required }
- Emits
  - verInfoPersonaje (char_id)
### DatosEntrada.vue
- Props
  - datos { type: Object, required }
  - id { type: Number, required }
- Emits
  - verInfoPersonaje (char_id)
### PersonajeInfo.vue
- Props
  - personaje_info { type: Any, required }
  - en_favoritos { type: Boolean, required }
