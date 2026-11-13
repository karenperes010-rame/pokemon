# Pokémon: Caos Total

Juego de retos por categorías para jugar en grupo, al estilo Kahoot. Cada
jugador se registra, elige un Pokémon y responde retos contra el tiempo.
Entre más rápido responda, más puntos gana. Las estadísticas de su Pokémon
multiplican los puntos según la categoría. Al final, el ranking muestra quién
va de último y la app le sortea una penitencia.

> Proyecto de la materia Multimedia para Móviles, hecho en Flutter.

**App en línea:** `https://<usuario>.github.io/<repositorio>/`
**Video de sustentación:** `https://youtu.be/<id>`
**Prototipo en Figma:** `https://www.figma.com/<enlace>`

---

## ¿Qué es?

Es un juego social para reuniones o clases. Varios jugadores se turnan el
mismo celular, compiten en seis categorías de retos y acumulan puntos. El
perdedor paga una penitencia sorteada por la app.

## Funcionalidades

- Registro de varios jugadores. Su puntaje se guarda en el dispositivo.
- Selección de Pokémon con buscador, usando datos reales de la **PokéAPI**.
- Seis categorías. Cada una está ligada a una estadística del Pokémon:

| Categoría | Estadística | Tiempo | Origen de las preguntas |
|---|---|---|---|
| Conocimiento Pokémon | Ataque especial | 15 s | Locales |
| ¿Quién es ese Pokémon? | Defensa | 10 s | PokéAPI (al azar) |
| Velocidad | Velocidad | 6 s | Locales |
| Memoria y observación | Defensa especial | 10 s | Locales (se muestran y se esconden) |
| Trivia gamer | PS | 20 s | Open Trivia DB |
| Modo caótico | Ataque | 20 s | Retos físicos que valida el grupo |

- **Puntaje tipo Kahoot:** `1000 × (1 − tiempo usado / tiempo total / 2) × bono del Pokémon`.
  Si respondes al instante ganas cerca de 1000 puntos, y si respondes al final, cerca de 500.
  Si fallas o se acaba el tiempo ganas 0 puntos, pero conservas los que tenías.
- **Bono del Pokémon:** `1 + estadística / 300`. Por ejemplo, Pikachu tiene 90 de
  velocidad, así que gana x1.30 en la categoría Velocidad.
- **Racha:** cada 3 aciertos seguidos suman +200 puntos.
- **Ranking** con líder y perdedor, y un **sorteo aleatorio de penitencias**.

## APIs usadas

1. **PokéAPI**: `https://pokeapi.co/api/v2/pokemon/{nombre o id}`. De ahí salen la
   imagen, los tipos y las estadísticas del Pokémon, y las preguntas de "¿Quién es ese Pokémon?".
2. **Open Trivia DB** (API libre, sin clave): `https://opentdb.com/api.php?amount=6&category=15&type=multiple`.
   De ahí salen las preguntas de videojuegos de la categoría "Trivia gamer".

## Estructura del código

```
lib/
├── main.dart                  # Tema, navegación (BottomNavigationBar) y lógica del juego
├── data/datos_juego.dart      # Categorías, preguntas locales y penitencias
├── models/
│   ├── categoria.dart         # Modelo de categoría + cálculo del multiplicador
│   └── jugador.dart           # Modelo de jugador (Pokémon, puntos, JSON)
├── services/
│   ├── pokeapi_service.dart   # API 1: PokéAPI
│   ├── trivia_service.dart    # API 2: Open Trivia DB
│   └── almacenamiento_service.dart  # Guardado local (shared_preferences)
├── screens/                   # 8 pantallas
│   ├── inicio.dart
│   ├── registro_jugadores.dart
│   ├── seleccion_pokemon.dart
│   ├── categorias.dart
│   ├── partida.dart
│   ├── resultados.dart
│   └── ranking.dart
├── widgets/                   # Widgets personalizados
│   ├── pokemon_card.dart
│   ├── pregunta_card.dart
│   ├── tarjeta_categoria.dart
│   ├── tarjeta_jugador.dart
│   ├── estadisticas_pokemon.dart
│   ├── encabezado_seccion.dart
│   └── dato_partida.dart
├── theme/colores.dart         # Paleta del sistema de diseño
└── utils/texto.dart           # Funciones de ayuda
assets/images/logo.png         # Imagen local (Image.asset)
```

## Cómo ejecutarlo

Requisitos: Flutter 3.27 o superior.

```bash
git clone https://github.com/<usuario>/<repositorio>.git
cd <repositorio>
flutter pub get
flutter run            # en un celular o emulador
flutter run -d chrome  # en el navegador
```

## Deploy

El archivo `.github/workflows/deploy.yml` compila la versión web y la publica en
**GitHub Pages** cada vez que se hace push a `main`. Para activarlo, en el repositorio
ve a *Settings → Pages → Source* y elige **GitHub Actions**.

---

## Manual de uso

1. **Inicio.** Toca **Comenzar partida**.
2. **Jugadores.** Escribe tu nombre y toca **Registrar y jugar**. Si ya estás
   registrado, toca tu nombre en la lista para jugar tu turno.
3. **Elige tu Pokémon.** Toca una tarjeta o busca uno por nombre (por ejemplo,
   *gengar*) y toca **Confirmar Pokémon**.
4. **Categorías.** Mira las estadísticas de tu Pokémon. Cada categoría muestra
   cuánto multiplica tus puntos (x1.30, por ejemplo). Toca la que quieras jugar.
5. **Partida.** Responde antes de que se acabe la barra de tiempo.
   - En **Memoria**, memoriza lo que aparece: se esconde a los 4 segundos.
   - En **¿Quién es ese Pokémon?**, adivina por la silueta.
   - En **Modo caótico**, haz el reto y el grupo decide si lo cumpliste.
6. **Resultados.** Ves cuántos puntos ganaste y tu total acumulado. Puedes jugar
   otra categoría o pasarle el turno al **siguiente jugador**.
7. **Ranking.** En la pestaña inferior **Ranking** ves la tabla de posiciones.
   Cuando han jugado al menos 2 personas, aparece el perdedor. Toca **Sortear
   penitencia** y que la cumpla.
8. **Nuevo torneo.** En el menú (⋮) del Ranking puedes poner los puntos en 0 o
   borrar todo.

   <img width="444" height="444" alt="WhatsApp Image 2026-11-13 at 12 38 13 AM" src="https://github.com/user-attachments/assets/c785d311-cd21-4aee-8ac5-5ee505b149a3" />


## Equipo

- Laura Jimenez
- Niyired Gonzalez
- Karen Pérez
- Sofia Reina
