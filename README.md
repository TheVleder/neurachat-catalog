# Catálogo de modelos de NeuraChat

`models.json` es el catálogo remoto que lee la app NeuraChat. Sirve para añadir
modelos nuevos y corregir precios o fechas de publicación **sin sacar una versión
nueva de la app**.

La app lo descarga de

```
https://raw.githubusercontent.com/TheVleder/neurachat-catalog/main/models.json
```

al abrirse, como mucho una vez cada 12 horas. Se puede forzar la descarga, o cambiar
la URL, en **Ajustes → Catálogo de modelos**. Si el archivo no está disponible, la app
sigue con el catálogo que lleva dentro.

## Formato

```json
{
  "version": 1,
  "updated": "2026-09-18",
  "models": [
    {"id": "gpt-5.6-terra", "provider": "openai", "label": "GPT-5.6 Terra",
     "context": 1050000, "vision": true, "reasoning": true,
     "released": "2026-07-09", "input": 2.0, "output": 12.0}
  ]
}
```

| Campo | Obligatorio | Qué es |
|---|---|---|
| `id` | sí | Identificador del modelo en la API del proveedor |
| `provider` | sí | `openai`, `anthropic`, `gemini`, `deepseek`, `kimi`, `minimax`, `groq`, `mistral`, `xiaomi` o `qwen` |
| `label` | sí | Nombre que se ve en la app |
| `context` | no | Ventana de contexto, en tokens |
| `vision` | no | Si acepta imágenes |
| `reasoning` | no | Si razona |
| `released` | no | Fecha de publicación, `AAAA-MM-DD` o `AAAA-MM` |
| `input` / `output` | no | Precio en USD por millón de tokens |

## Cómo se aplica

- Un modelo que ya está en la app toma los campos que vengan aquí. Uno nuevo se añade
  al final de su proveedor.
- Los precios de este archivo mandan sobre los de la app, **salvo** los que el usuario
  haya cambiado a mano.
- Una entrada inválida se ignora y el resto del archivo se aplica igual.

Al cambiar este archivo, actualiza también `updated`.
