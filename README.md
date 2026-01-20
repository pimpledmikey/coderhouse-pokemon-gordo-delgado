coderhouse-pokemon-gordo-delgado

Proyecto: Pre-entrega CoderHouse — Pokemon Weight Checker

Descripción
Este repositorio contiene la pre-entrega del curso: un workflow de n8n que recibe un `pokemonId` por webhook, consulta la PokéAPI, evalúa si el Pokémon es "pesado" (peso > 50 kg) y envía una notificación por email.

Estructura

/pre-entrega
├── workflow_preentrega.json   # Workflow exportado de n8n
├── README_preentrega.md      # Documentación para la entrega
└── evidencias/
    └── captura_1.png         # Evidencias (captura del workflow o Execution Log)

Instrucciones rápidas
1. Importar `pre-entrega/workflow_preentrega.json` en n8n Cloud.
2. Configurar la credencial SMTP en n8n (Gmail App Password) y guardar con el id `helpbinfo_smtp`.
3. Activar el workflow y probar con curl contra la URL de webhook (ejemplo en README_preentrega.md).

Notas de seguridad
- No subir credenciales al repositorio. Las credenciales deben guardarse únicamente en el gestor de n8n.
- He sanitizado el campo `sendTo` en el workflow y configurado un fallback, pero usá una dirección real para las pruebas.

Autor: Miguel Requena
Fecha: Enero 2026
