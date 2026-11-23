# 📱 Nexus 11 - Red Social Multiplataforma

![Kotlin](https://img.shields.io/badge/kotlin-%237F52FF.svg?style=for-the-badge&logo=kotlin&logoColor=white)
![Android](https://img.shields.io/badge/Android-3DDC84?style=for-the-badge&logo=android&logoColor=white)
![iOS](https://img.shields.io/badge/iOS-000000?style=for-the-badge&logo=ios&logoColor=white)
![Compose Multiplatform](https://img.shields.io/badge/Compose_Multiplatform-000000?style=for-the-badge&logo=Jetpack+Compose&logoColor=white)

Nexus 11 es una aplicación móvil multiplataforma (iOS y Android) desarrollada con **Kotlin Multiplatform (KMP)** y **Compose Multiplatform**. 

Diseñada como Proyecto Final de Ciclo (DAM), esta red social demuestra la implementación de arquitecturas modernas, compartiendo la lógica de negocio y una interfaz gráfica (UI) 100% reactiva y unificada desde un único código base.

## ✨ Funcionalidades Principales

### 🔄 Feed Dinámico y Social
* **Algoritmo de filtrado:** Pestañas de contenido global (Descubrir), red de contactos (Siguiendo) y sugerencias inteligentes (Para ti) basadas en afinidad de perfil.
* **Interacciones en tiempo real:** Sistema de *Likes* y comentarios integrados en cada publicación.
* **Publicaciones ricas:** Creación de posts con texto (límite de 280 caracteres con indicador visual) y carga de imágenes desde la galería del dispositivo.
* **Pull-to-refresh:** Carga bajo demanda de nuevo contenido.

### 💬 Mensajería Avanzada (Chats)
* **Conversaciones activas:** Bandeja de entrada con indicadores de mensajes no leídos.
* **Interacción fluida:** Soporte para enviar texto e imágenes.
* **Acciones de mensaje:** Gestos nativos como *swipe-to-reply* (deslizar para responder), además de edición, eliminación y reacciones con emojis (❤️ 😂 😮 👍) mediante pulsación larga.

### 🎨 Personalización y Estado Global
* **Theming Dinámico:** Modificación del "Color de Acento" que propaga el cambio de estado a toda la UI de la aplicación de forma instantánea.
* **Fondos personalizados:** Soporte para diferentes temas en las salas de chat (Oscuro, Océano, Galaxia).

### 👤 Gestión de Perfil
* Edición completa de biografía, avatar, profesión y *Vibe* mediante un sistema de etiquetas visuales.
* Buscador de usuarios integrado para explorar la red y gestionar seguimientos.

## 🛠️ Stack Tecnológico

| Área | Tecnología |
|------|-----------|
| Lenguaje | Kotlin 2.0 |
| UI y lógica compartida | Kotlin Multiplatform + Compose Multiplatform |
| Navegación | Voyager (navigator, tabs y transiciones) |
| Red | Ktor Client (OkHttp en Android, Darwin en iOS) + kotlinx.serialization |
| Backend / datos | Firebase Authentication (JWT) + Realtime Database, vía API REST |
| Imágenes | Kamel (carga) y Peekaboo (selector de galería) |
| Persistencia local | multiplatform-settings |
| Fechas | kotlinx-datetime |

## 🧱 Estructura del proyecto

```
composeApp/src/
├── commonMain/kotlin/com/example/nexus11/
│   ├── data/        # Repositorios (auth, chat, datos), caché y modelos (User, Post, Mensaje, Story)
│   ├── ui/
│   │   ├── screens/ # auth, home, chat, post, profile, splash
│   │   └── theme/   # Colores y tema dinámico
│   └── utils/       # Utilidades (hash de contraseñas)
├── androidMain/     # Punto de entrada y código específico de Android
└── iosMain/         # Punto de entrada y código específico de iOS
iosApp/              # Proyecto Xcode que aloja la app en iOS
```

La lógica de negocio, los repositorios y toda la interfaz viven en `commonMain` y se comparten entre Android e iOS. Solo lo estrictamente específico de cada plataforma está en `androidMain` e `iosMain`.

## 🚀 Cómo ejecutar el proyecto

**Requisitos:** Android Studio (o IntelliJ IDEA) con el plugin de Kotlin Multiplatform, JDK 17+ y, para iOS, macOS con Xcode.

### Android
Desde el IDE con la configuración de `composeApp`, o desde la terminal:

```bash
./gradlew :composeApp:assembleDebug
```

En Windows: `gradlew.bat :composeApp:assembleDebug`.

### iOS
Abre `iosApp/iosApp.xcodeproj` en Xcode y ejecuta el esquema `iosApp` en un simulador o dispositivo.

## ⚠️ Limitaciones conocidas y mejoras previstas
Es un proyecto académico y estas son las cosas que mejoraría en una siguiente versión:

- **Configuración:** la URL de la base de datos y la clave de Firebase están escritas en el código y repartidas en varios repositorios (`AuthRepository`, `DataRepository`, `ChatRepository`, `Config`). Pasarlas a un único punto de configuración por entorno.
- **Contraseñas:** la app aplica un hash SHA-256 a la contraseña antes de enviarla a Firebase Auth. Firebase ya se encarga de guardarla de forma segura, así que ese paso es innecesario y habría que quitarlo.
- **Tests:** solo existe el test de ejemplo de la plantilla. Faltan tests de los repositorios y de la lógica compartida en `commonTest`.
- **Arquitectura:** los repositorios acceden directamente a la API REST. Un siguiente paso sería separar una capa de dominio e inyectar dependencias (por ejemplo con Koin).

## 📌 Notas
Proyecto Final de Ciclo (DAM). El backend usa una instancia de Firebase Realtime Database pensada para desarrollo y demostración.
