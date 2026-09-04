# Clases-n8n

# 🚀 Automatizaciones y Laboratorios en n8n

Este repositorio recopila los flujos de trabajo desarrollados durante las clases prácticas de n8n, abarcando desde integraciones básicas con mensajería y APIs externas hasta la construcción de webhooks, flujos condicionales y Agentes de Inteligencia Artificial avanzados.

---

## 📂 Contenido del Repositorio

### 1. My workflow (`My workflow.json`)
* **Qué hace:** Es un flujo de prueba básico e inicial. Utiliza un disparador manual (`Manual Trigger`)[cite: 1], pasa por un nodo de edición de campos (`Edit Fields`) para asignar un texto estático ("ooooooo") a una variable[cite: 1], y finalmente envía este mensaje directamente a un chat de Telegram configurado[cite: 1].
* **Relación con otros:** Funciona de manera independiente como una plantilla o ejercicio introductorio de prueba rápida para conectar n8n con Telegram.

---

### 2. S13 - Control de Solicitudes (`S13 - Control de Solicitudes.json`)
* **Qué hace:** Simula un sistema de gestión de tickets o mesa de ayuda de forma interna. Inicia con un disparador manual que define los datos de un solicitante (nombre, tipo, problema y prioridad numérica)[cite: 2]. Utiliza un nodo condicional (`If`) para evaluar si la prioridad es alta (mayor o igual a 8)[cite: 2], procesa el mensaje correspondiente mediante nodos de asignación y unifica los caminos con un nodo `Merge` para notificar el resultado por Telegram[cite: 2].
* **Relación con otros:** Este flujo es la versión base y manual de la *Semana 13*. Comparte la misma lógica de negocio que `S13 - Control de Solicitudes (Form + Telegram + Gmail).json`, pero en lugar de recibir los datos mediante un formulario web, utiliza variables internas predefinidas[cite: 2, 5].

---

### 3. S13 - Alerta Clima (`S13 - Alerta Clima.json`)
* **Qué hace:** Automatiza la consulta meteorológica en tiempo real consumiendo la API pública de *Open-Meteo* para Bogotá[cite: 3]. Extrae datos clave como la temperatura y la precipitación actual[cite: 3], evalúa mediante un condicional si está lloviendo (precipitación > 0)[cite: 3], y genera una alerta diferenciada que se unifica con un nodo `Merge` para enviarla por Telegram[cite: 3].
* **Relación con otros:** Es un flujo completamente independiente enfocado en integraciones con APIs externas y lógica condicional basada en datos meteorológicos.

---

### 4. S13 - Reto TRM Colombia (`S13 - Reto TRM Colombia.json`)
* **Qué hace:** Consulta periódicamente o de forma manual la Tasa Representativa del Mercado (TRM) oficial de Colombia utilizando la API de *DolarAPI*[cite: 4]. Extrae los valores financieros[cite: 4] y evalúa mediante una condición si el valor supera o cumple un umbral determinado para disparar alertas financieras o reportes diarios hacia Telegram[cite: 4].
* **Relación con otros:** Comparte la misma temática de la *Semana 13* orientada al consumo de APIs financieras y notificaciones automatizadas, operando de forma autónoma respecto a los demás flujos.

---

### 5. S13 - Control de Solicitudes (Form + Telegram + Gmail) (`S13 - Control de Solicitudes (Form + Telegram + Gmail).json`)
* **Qué hace:** Eleva el nivel de la mesa de ayuda de la sesión 13 integrando un formulario web interactivo (`n8n Form Trigger`)[cite: 5]. Los usuarios ingresan sus datos de soporte directamente[cite: 5], el sistema evalúa la prioridad[cite: 5], notifica al administrador por Telegram y, de forma complementaria, genera y envía un correo electrónico formateado en HTML mediante *Gmail*[cite: 5].
* **Relación con otros:** **Va de la mano directamente con** `S13 - Control de Solicitudes.json`. Representa la evolución natural de ese flujo: reemplaza el disparador manual por un formulario real y amplía los canales de salida añadiendo el envío de correos corporativos/personales automatizados.

---

### 6. S14_Lab1_Webhook_GET (`S14_Lab1_Webhook_GET.json`)
* **Qué hace:** Configura un endpoint web personalizado mediante el método HTTP GET (`Webhook GET`) bajo la ruta `saludo-api`[cite: 6]. Captura los parámetros enviados a través de la URL (`query parameters` como nombre y curso), procesa una cadena de texto personalizada y responde directamente al cliente utilizando el nodo `Respond to Webhook`[cite: 6].
* **Relación con otros:** Es el primer laboratorio introductorio al uso de Webhooks en la *Semana 14*, sirviendo como base conceptual para entender cómo n8n puede actuar como un servidor API liviano.

---

### 7. S14_Lab3_Cliente_Solicitudes (`S14_Lab3_Cliente_Solicitudes.json`)
* **Qué hace:** Actúa como un cliente HTTP externo simulando el envío de una petición POST con un cuerpo JSON estructurado (datos de un usuario con problemas de acceso y prioridad alta) hacia un servidor o endpoint de n8n[cite: 7].
* **Relación con otros:** **Va de la mano de forma estricta con** `S14_Lab3_Receptor_Solicitudes.json`. Este archivo (`Cliente`) cumple el rol de emisor o cliente que dispara la petición de prueba, mientras que el archivo *Receptor* es el encargado de recibirla, procesarla y notificarla.

---

### 8. S14_Lab3_Receptor_Solicitudes (`S14_Lab3_Receptor_Solicitudes.json`)
* **Qué hace:** Funciona como el servidor o backend receptor. Escucha peticiones entrantes por el método POST en la ruta `solicitud-soporte`[cite: 8], extrae los campos del cuerpo de la petición (`Edit Fields`)[cite: 8], envía una notificación interna a Telegram con los detalles del ticket[cite: 8], and finalmente devuelve una respuesta de confirmación al cliente (`Respond to Webhook`)[cite: 8].
* **Relación con otros:** **Va de la mano y complementa directamente a** `S14_Lab3_Cliente_Solicitudes.json`. Mientras el cliente genera la solicitud de prueba, este flujo la procesa y cierra el ciclo de comunicación cliente-servidor.

---

### 9. S14_Reto_API_Departamento (`S14_Reto_API_Departamento.json`)
* **Qué hace:** Crea un Webhook GET personalizado (`consulta-departamento`) que recibe el nombre de un departamento colombiano como parámetro[cite: 9]. Utiliza un nodo HTTP Request para consultar la pasarela oficial de *API-Colombia*, procesa datos demográficos y de superficie (población, municipios, área) y devuelve un resumen formateado como texto plano al cliente que hizo la petición[cite: 9].
* **Relación con otros:** Se alinea con los laboratorios de la *Semana 14* sobre Webhooks, combinando la recepción de peticiones mediante GET con el consumo dinámico de una API externa especializada.

---

### 10. AI Agent con Gemini y Calculator (`AI Agent con Gemini y Calculator.json`)
* **Qué hace:** Implementa un Agente de Inteligencia Artificial básico utilizando nodos de *LangChain* en n8n[cite: 10]. Integra un disparador de chat[cite: 10], un modelo de lenguaje de Google Gemini configurado con System Messages específicos[cite: 10], y una herramienta de cálculo (`Calculator Tool`)[cite: 10] que le permite al modelo delegar operaciones matemáticas de forma autónoma.
* **Relación con otros:** Sirve como la primera toma de contacto e introducción al desarrollo de Agentes inteligentes dentro de n8n con LangChain.

---

### 11. S15_Lab1_Agente_Gemini (`S15_Lab1_Agente_Gemini.json`)
* **Qué hace:** Configura un Agente de Inteligencia Artificial basado en Gemini enfocado en la tutoría de estudiantes[cite: 11]. Incorpora un sistema de memoria a corto plazo (`Window Buffer Memory`)[cite: 11], una herramienta de cálculo matemática (`Calculator`)[cite: 11] y un conector HTTP especializado (`HTTP Request1`) que actúa como herramienta externa para consultar la TRM de Colombia en tiempo real de forma dinámica bajo demanda del agente[cite: 11].
* **Relación con otros:** Evoluciona los conceptos del Agente básico anterior añadiendo memoria conversacional persistente por sesión y múltiples herramientas integradas de consulta externa.

---

### 12. S15_Lab3_Agente_Telegram_Fixed_Session (`S15_Lab3_Agente_Telegram_Fixed_Session.json`)
* **Qué hace:** Implementa un Agente de IA completo integrado directamente con *Telegram* (`Telegram Trigger` y `Telegram Send Message`)[cite: 12]. Utiliza un sistema de memoria optimizado (`Simple Memory`) basado en el ID del chat del usuario para mantener el contexto de la conversación[cite: 12], integra la herramienta de operaciones matemáticas (`Calculator`)[cite: 12] y añade conexión a *Google Sheets* (`Google Sheets Tool`) para consultar filas y registros de una hoja de cálculo en la nube como fuente de datos[cite: 12]. El agente está sujeto a reglas estrictas de formato (texto plano sin markdown) para evitar errores de envío en Telegram[cite: 12].
* **Relación con otros:** Representa un flujo de producción completo de la *Semana 15*, conectando un canal de mensajería real (Telegram), bases de conocimiento dinámicas (Google Sheets) y motores de razonamiento con IA.
