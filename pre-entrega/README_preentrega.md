
# Pre-entrega CoderHouse — Pokemon Weight Checker

Nombre del caso
Pokemon Weight Checker — clasifico un Pokémon por peso y envío una notificación por correo.

Qué dispara el workflow (trigger)
Un Webhook POST que recibe un `pokemonId` opcional y un `email` de destino. Si no se envía `pokemonId` se genera uno aleatorio.

Descripción breve de los nodos
- `Webhook Trigger`: recibe la petición POST con `pokemonId` y `email`.
- `Set Pokemon ID`: normaliza el ID recibido o genera un ID aleatorio entre 1 y 150.
- `Pokemon API Request`: consulta la PokéAPI pública `https://pokeapi.co/api/v2/pokemon/{id}`.
- `Transformar Datos Pokemon`: extrae `nombre`, `peso`, `altura`, `tipo` e `imagen` y los deja en campos limpios.
- `IF Pokemon Pesado`: evalúa si `peso > 500` (la API devuelve hectogramos, por eso 500 = 50 kg).
- `Preparar Alerta Pesado` / `Preparar Info Ligero`: construyen el asunto y el cuerpo del email según la rama.
- `Enviar Email Pesado` / `Enviar Email Ligero`: envían el email usando la credencial SMTP configurada en n8n.
- `Respuesta Webhook`: devuelve un JSON con resumen de la ejecución.

Qué evalúa el condicional y por qué
Se evalúa `peso > 500` porque la PokéAPI devuelve el peso en hectogramos (1 hg = 0.1 kg). 500 hg equivale a 50 kg, que uso como umbral para considerar un Pokémon como "pesado".

Cómo configuré la notificación
Usé SMTP con Gmail. En n8n añadí una credencial SMTP con host `smtp.gmail.com`, puerto `465`, usuario y App Password. El campo `From` coincide con la cuenta configurada en la credencial.

Buenas prácticas aplicadas

- No expongo credenciales en los archivos exportados; las guardo en el gestor de credenciales de n8n.
- Manejo de fallback: si no se envía `pokemonId` o `email`, el workflow tiene valores por defecto para permitir pruebas.

- Las respuestas y logs se registran en Execution Log de n8n para depuración.

Cómo probar (resumen)
1. Importar `workflow_preentrega.json` en n8n Cloud.
2. Configurar la credencial SMTP en n8n (Gmail App Password).
3. Activar el workflow.
4. Enviar un POST a la URL del webhook (ejemplo con la URL de producción):

```bash
curl -X POST 'https://codersh.app.n8n.cloud/webhook/pokemon-check' \
  -H 'Content-Type: application/json' \
  -d '{"pokemonId":143,"email":"tu_email@dominio.com"}'
```

Estructura de entrega

```
/pre-entrega
├── workflow_preentrega.json
├── README_preentrega.md
└── evidencias/
    └── captura_1.png
```

Autor: Miguel Requena