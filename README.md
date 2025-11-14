IADetector - Verificador Instantáneo de Texto IA

IADetector es una herramienta web front-end simple, rápida y centrada en la privacidad, diseñada para una demostración de concepto de detección de texto generado por inteligencia artificial.

Este proyecto prioriza la velocidad, la facilidad de uso y una interfaz de usuario limpia. No requiere registros, no almacena datos del usuario y ofrece un resultado visual e inmediato.

Nota Importante: La lógica de detección en esta versión es una simulación. Está diseñada para demostrar el flujo completo de la interfaz de usuario (estados de carga, mensajes de error, visualización de resultados) sin necesidad de una API o un modelo de backend.

🚀 Características Principales

Análisis Instantáneo (Simulado): Pega un texto y obtén un resultado en segundos.

Interfaz Clara y Visual: Un resultado en porcentaje con un código de color claro (Verde para Humano, Ámbar para Mixto, Rojo para IA).

Sin Registros: Totalmente gratuito y anónimo. No se requiere email ni cuenta.

Enfocado en la Privacidad: El análisis se simula localmente en el cliente. Ningún texto se envía a un servidor.

Diseño Responsive: Funciona perfectamente en dispositivos móviles y de escritorio.

Validación Simple: Contador de caracteres y deshabilitación del botón de análisis si no se cumple el mínimo de 50 caracteres.

💻 Tecnologías Utilizadas

Este proyecto es deliberadamente simple y se ejecuta en un único archivo, sin necesidad de un build process:

HTML5: Para la estructura semántica.

Tailwind CSS (vía CDN): Para todo el diseño y la interfaz de usuario responsive.

JavaScript (ES6+): Para toda la lógica de la interfaz, manejo de eventos, validación y la simulación de la llamada a la API.

🛠️ Cómo Usarlo

No hay un proceso de instalación. Puedes usarlo de dos maneras:

1. Verlo en Acción (GitHub Pages)

Si subes este repositorio a GitHub, puedes activar GitHub Pages fácilmente:

Ve a la pestaña Settings de tu repositorio.

Ve a la sección Pages.

Elige la rama main (o master) y la carpeta /root.

¡Guarda y tu sitio estará activo en https://tu-usuario.github.io/iadetector/iadetector.html!

2. Ejecución Local

Clona este repositorio:

git clone [https://github.com/tu-usuario/iadetector.git](https://github.com/tu-usuario/iadetector.git)


Navega al directorio del proyecto:

cd iadetector


Simplemente abre el archivo iadetector.html en tu navegador web preferido (Chrome, Firefox, Safari, etc.).

🔮 Futuras Mejoras (Implementación Real)

El brief original sugería APIs reales. Para convertir esta demostración en una herramienta funcional, el siguiente paso sería reemplazar la función simulateApiCall() en el <script> de iadetector.html.

La función actual es:

// --- Simulación de la API ---
function simulateApiCall(text) {
    return new Promise(resolve => {
        // ...lógica de retraso y resultado aleatorio...
        resolve({ percentage, confidence });
    });
}


Esta función debería ser reemplazada por una llamada fetch a una API de detección de IA real, por ejemplo:

Opción 1: Hugging Face (Modelo RoBERTa)

async function analyzeTextWithHuggingFace(text) {
    const API_URL = '[https://api-inference.huggingface.co/models/roberta-base-openai-detector](https://api-inference.huggingface.co/models/roberta-base-openai-detector)'; // Ejemplo de modelo
    const API_TOKEN = 'hf_TU_TOKEN_AQUI'; // Reemplazar con tu token
    
    const response = await fetch(API_URL, {
        method: 'POST',
        headers: { 
            'Authorization': `Bearer ${API_TOKEN}`,
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({ inputs: text })
    });
    
    if (!response.ok) {
        throw new Error(`Error de API: ${response.statusText}`);
    }
    
    const result = await response.json();
    // Procesar el 'result' para que coincida con el formato { percentage, confidence }
    // Ejemplo (puede variar mucho según el modelo):
    // const aiScore = result[0].find(label => label.label === 'LABEL_1').score; // Asumiendo que LABEL_1 es IA
    // return { percentage: Math.floor(aiScore * 100), confidence: 'Alta' };
}


Opción 2: Modelo Local con TensorFlow.js
Esto implicaría cargar un modelo (model.json) y sus pesos, y ejecutar la predicción localmente, lo cual mantendría el beneficio de la privacidad.

📜 Licencia

Este proyecto está bajo la Licencia MIT. Consulta el archivo LICENSE (puedes añadir uno) para más detalles.
