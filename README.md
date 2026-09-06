# Watch-skill

Le da a Claude la capacidad de "ver" un video (URL o archivo local): lo descarga con
`yt-dlp`, extrae frames con `ffmpeg`, obtiene la transcripción (captions nativos o
Whisper como respaldo) y entrega todo eso para que Claude pueda responder preguntas
sobre lo que pasa en pantalla — no solo lo que se dice.

La skill (`skills/watch/`) es la skill **watch** del proyecto
[bradautomates/claude-video](https://github.com/bradautomates/claude-video),
incluida acá tal cual (licencia MIT) como unidad autocontenida para poder
instalarla/usarla directamente desde este repo. Ver `skills/watch/SKILL.md` para
el detalle completo del flujo y `LICENSE` para la licencia original.

## Instalar

**Claude Code (plugin marketplace del proyecto original):**

```
/plugin marketplace add bradautomates/claude-video
/plugin install watch@claude-video
```

**Cualquier host compatible con Agent Skills (Codex, Cursor, Copilot, Gemini CLI, etc.):**

```bash
npx skills add bradautomates/claude-video -g
```

**Manual / directo desde este repo:**

```bash
git clone https://github.com/SebasSuarez22/watch-skill.git
ln -s "$(pwd)/watch-skill/skills/watch" ~/.claude/skills/watch
```

## Primer uso

En la primera invocación, `scripts/setup.py --check` verifica que `ffmpeg` y
`yt-dlp` estén disponibles y guía la instalación si faltan (macOS vía `brew`,
Linux imprime los comandos `apt`/`dnf`/`pipx` exactos, Windows `winget`/`pip`).
Whisper (transcripción de respaldo cuando el video no tiene captions) requiere
una `GROQ_API_KEY` o `OPENAI_API_KEY` en `~/.config/watch/.env`.

## Uso

```
/watch <url-o-ruta-del-video> [pregunta opcional]
```

Ejemplos:

```
/watch https://youtube.com/watch?v=XXXX ¿qué marca de zapatillas usa en el minuto 3?
/watch https://youtube.com/watch?v=XXXX resumime el video con marcas de tiempo
```
