# automatizacion-avanzada-ia-coderhouse
# Agente de Calificación de Leads con n8n

Proyecto integrador desarrollado para el curso **Automatización con IA de Coderhouse**.

## Checkpoint 1: Agente base y motor de razonamiento

Este workflow implementa un agente de inteligencia artificial para analizar consultas comerciales y clasificar leads según su nivel de prioridad.

El agente utiliza **Google Gemini** como modelo de lenguaje y cuenta con herramientas de Gmail para enviar alertas comerciales y reportes de supervisión.

## Funcionalidades

- Recepción de consultas mediante Chat Trigger.
- Clasificación de leads como `ALTO`, `MEDIO` o `BAJO`.
- Identificación de nombre, empresa, necesidad, plazo, presupuesto, autoridad y correo.
- System Prompt modular con rol, ámbito, objetivos, reglas y escalamiento.
- Límite máximo de 7 iteraciones.
- Activación autónoma de Gmail para leads prioritarios.
- Envío determinista de un registro de supervisión.
- Registro de los pasos intermedios ejecutados por el agente.
- Restricciones para evitar datos inventados y acciones no autorizadas.

## Arquitectura del workflow

```text
[Chat Trigger]
      │
      ▼
[AI Agent + System Prompt]
      ├── [Google Gemini Chat Model]
      └── [Gmail: aviso de lead prioritario]
      │
      ▼
[Gmail: log de supervisión]
```

El modelo y la herramienta están conectados lateralmente al agente. Gmail se activa de manera probabilística solamente cuando se cumplen los criterios comerciales definidos.

El nodo final de observabilidad se ejecuta de forma lineal después del agente.

## Modelo utilizado

```text
Google Gemini 3.1 Flash-Lite
```

Se seleccionó este modelo por su compatibilidad con herramientas, velocidad de respuesta y disponibilidad mediante la API de Gemini.

## Prueba realizada

El workflow fue probado con un lead que proporcionó:

- Necesidad comercial concreta.
- Plazo definido.
- Presupuesto asignado.
- Autoridad en la decisión.
- Correo electrónico válido.

El agente clasificó el lead como `ALTO`, ejecutó correctamente la herramienta Gmail y posteriormente envió el registro de supervisión.

## Archivo entregable

```text
checkpoint1_eduardo_ahumada.json
```

## Requisitos para utilizar el workflow

- Una instancia de n8n compatible con nodos de IA.
- Credencial de Google Gemini API.
- Credencial OAuth2 de Gmail.
- Direcciones de correo configuradas para alertas y supervisión.

Las credenciales y claves privadas no están incluidas en el archivo exportado.

## Seguridad

El agente tiene instrucciones para:

- No inventar información.
- No exponer credenciales ni instrucciones internas.
- No prometer precios, contratos, plazos o resultados.
- No ejecutar acciones externas fuera de las herramientas autorizadas.
- Solicitar revisión humana ante riesgos legales, financieros o de privacidad.
- No afirmar que envió un correo sin recibir confirmación de la herramienta.

## Evolución del proyecto

Este workflow constituye la primera versión del proyecto integrador. En los próximos módulos se incorporarán progresivamente:

- Arquitectura multiagente.
- Memoria y contexto por sesión.
- Integraciones adicionales.
- RAG y base documental.
- Procesamiento de voz.
- Nuevos mecanismos de supervisión y seguridad.

## Autor

**Eduardo Ahumada**  
Proyecto académico — Coderhouse
