# ClawMobil 🦞

Convierte cualquier teléfono Android antiguo en un **servidor de IA personal** con [OpenClaw](https://github.com/erbolamm/openclaw). Sin cloud. Sin suscripciones. Tu propio cerebro digital de bolsillo.

**Web**: [ApliArte.com](https://apliarte.com) · **#ClawMobil**

---

## 🍜 Filosofía: El Wok

Este proyecto funciona como un **self-service**: tú descargas el proyecto (el buffet), creas tu carpeta personal, y vas cogiendo lo que necesitas — sin tocar nada del proyecto en sí.

| Carpeta | Qué es | ¿Se modifica? |
|---|---|---|
| `scripts/` | Scripts de instalación, evaluación y promoción | ❌ No |
| `termux_scripts/` | Scripts que se suben al Android | ❌ No |
| `config/` | Plantilla de configuración | ❌ No (copiar y personalizar) |
| `empezar.html` | Asistente web (prompt + perfil local) | ❌ No |
| **`Mis_configuraciones_locales/`** | **Tu bandeja personal** | ✅ Sí, solo esta |

> **Regla de oro**: si necesitas guardar una clave, un log, una nota, **o el código fuente de una App Flutter** (ej. un chat) que controla un dispositivo específico → va TODO dentro de `Mis_configuraciones_locales/dispositivos/<dispositivo>/`. El resto del proyecto madre se queda intacto. De esta manera, tu carpeta de dispositivo se convierte en un proyecto independiente que te puedes llevar a donde quieras.

---

## 🚀 Empezar (3 pasos)

### 1. Clona el proyecto
```bash
git clone https://github.com/erbolamm/ClawMobil.git
cd ClawMobil
```

### 2. Crea tu carpeta personal
```bash
mkdir -p Mis_configuraciones_locales/dispositivos/mi_dispositivo
cp Mis_configuraciones_locales/dispositivos/_plantilla/* \
   Mis_configuraciones_locales/dispositivos/mi_dispositivo/
```

Esta carpeta ya está en `.gitignore` — nada de lo que pongas ahí se sube al repo.

### 3. Conecta tu Android y despliega
1. Habilita **Depuración USB** en tu teléfono.
2. Conéctalo por cable al Mac/PC.
3. Abre **`index.html`** (entrada simplificada) y desde ahí entra a **`empezar.html`**.
4. Usa el **Asistente de Configuración Local** para generar:
   - `config_profile.json`
   - Prompt de despliegue
   - Comando para crear tu carpeta local.
5. Pega el prompt en tu IDE con IA (Cursor, Windsurf, Gemini, etc.).
6. Tu asistente IA ejecutará los scripts automáticamente.

## 🧭 Raíz simplificada para usuarios

Si vas a usar ClawMobil sin perfil técnico, en la raíz del proyecto céntrate solo en:

- `index.html` → flujo guiado para abrir VS Code y lanzar el asistente.
- `LEEME.md` → guía breve de operación modular.

El resto de carpetas/archivos existen para el funcionamiento interno del framework.

---

## 🧩 Modo Framework Local (fork/clon)

ClawMobil incluye un flujo modular para que cada fork o dispositivo trabaje con
su configuración local y, si descubre mejoras, pueda proponerlas a la plantilla:

```bash
# 1) Detectar configuración activa
bash scripts/local_config_select.sh

# 2) Evaluar completitud de perfiles locales
bash scripts/local_config_evaluate.sh

# 3) Detectar candidatos reutilizables vs _plantilla
bash scripts/local_config_discovery.sh

# 3.1) Detector automático de cambios locales
bash scripts/local_config_watch.sh

# 4) Promover una mejora de forma trazable
bash scripts/local_config_promote.sh <dispositivo> <ruta_relativa>

# 5) Crear snapshot/revertir pruebas
bash scripts/local_config_lab.sh snapshot <dispositivo>
bash scripts/local_config_lab.sh restore <dispositivo> <snapshot.tar.gz>

# 6) Prueba integral del flujo modular
bash scripts/local_config_selftest.sh

# 7) Smoke test del wizard (empezar.html)
bash scripts/wizard_local_smoketest.sh

# 8) Checklist pre-directo completo
bash scripts/prelive_direct_check.sh
```

Guía completa: [`docs/LOCAL_CONFIG_FRAMEWORK.md`](docs/LOCAL_CONFIG_FRAMEWORK.md)
Auditoría upstream: [`docs/AUDITORIA_OPENCLAW_ORIGINAL_2026-02-27.md`](docs/AUDITORIA_OPENCLAW_ORIGINAL_2026-02-27.md)
Guion directo: [`docs/GUION_DIRECTO_CLAWMOBIL_2026-02-27.md`](docs/GUION_DIRECTO_CLAWMOBIL_2026-02-27.md)

## 🔒 Dependencia OpenClaw prioritaria

Para estabilidad del framework, la referencia de motor se fija en el fork:

- <https://github.com/erbolamm/openclaw>

## 🔗 Vinculación ClawMobil ↔ fork OpenClaw

Este proyecto ClawMobil y el fork `erbolamm/openclaw` se están actualizando en paralelo para asegurar compatibilidad real con móviles antiguos reacondicionados.

Perfil de dispositivos validados en campo:

- Samsung (legacy)
- YesTeL Note series
- Huawei P10

En el fork se añadió un flujo reproducible de instalación para Android antiguos (Termux + ADB + SSH), pensado para que la comunidad pueda reutilizarlo sin depender de hardware nuevo:

- <https://github.com/erbolamm/openclaw/blob/main/docs/legacy-termux-android.md>
- <https://github.com/erbolamm/openclaw/blob/main/scripts/legacy/deploy-termux-via-adb.sh>

---

## 🛠️ ¿Qué consigues?

- **Chat por voz** — Habla con tu dispositivo y recibe respuestas inteligentes.
- **Visión IA** — La cámara del teléfono + IA = describe lo que ve.
- **IA 100% Offline** — Funciona sin internet con Ollama + Whisper.
- **Servidor 24/7** — Accesible por Telegram, API REST, o la app Flutter.
- **Smart Display** — Convierte el teléfono en una pantalla inteligente.
- **Avatar animado** — Cara de neón que reacciona a tus interacciones.

## 📋 Requisitos mínimos

- Android 7+ con al menos **3 GB de RAM** (4 GB+ para modo offline).
- **Restablecimiento de fábrica recomendado** — no uses tu teléfono principal.
- Cable USB y un Mac/PC para la configuración inicial.
- [Termux (F-Droid)](https://f-droid.org/packages/com.termux/) instalado en el Android.

## 📂 Estructura del proyecto

```
ClawMobil/
├── empezar.html              ← Generador de prompt de despliegue
├── index.html                ← Web pública del proyecto
├── scripts/                  ← Scripts de despliegue + framework local
├── termux_scripts/           ← Scripts que se suben al dispositivo
├── config/                   ← Plantilla de configuración
├── docs/                     ← Guías del framework (fork, local config)
├── lib/                      ← App Flutter (cliente)
├── Mis_configuraciones_locales/  ← 🔒 TU carpeta (gitignored)
│   ├── claves_globales.env
│   └── dispositivos/
│       ├── _plantilla/       ← Copia esto para cada nuevo dispositivo
│       └── tu_dispositivo/
│           ├── config_profile.json ← Perfil generado por wizard
│           ├── claves.env    ← Tus API keys
│           ├── notas.md      ← Estado y documentación
│           └── ...
```

## Autor

Javier Mateo (ApliArte) — [github.com/erbolamm](https://github.com/erbolamm)

## 💬 Una nota personal del autor / A personal note from the author

ℹ️ Nota: El texto siguiente es un mensaje personal del autor, escrito en varios idiomas para que pueda leerlo gente de todo el mundo. Esto no implica que el proyecto tenga soporte funcional completo en esos idiomas.

ℹ️ Note: The text below is a personal message from the author, written in several languages so people around the world can read it. This does not imply full multilingual feature support in those languages.

<details>
<summary>🇪🇸 Español</summary>

ClawMobil nació de una idea simple: los móviles viejos no deberían acabar en un cajón. Millones de dispositivos con procesadores capaces se quedan olvidados porque ya no reciben actualizaciones. Yo quise darles una segunda vida convirtiéndolos en servidores de inteligencia artificial personales.

Este proyecto lo construí solo, aprendiendo a programar desde cero desde abril de 2023. No hay empresa detrás, no hay inversores, no hay equipo de marketing. Solo un programador español que cree que la tecnología debe ser accesible para todos.

Si ClawMobil te resulta útil, compártelo. Cada persona que lo descubre es una victoria. Y si quieres apoyar el desarrollo, un café siempre ayuda. ❤️
</details>

<details>
<summary>🇬🇧 English</summary>

ClawMobil was born from a simple idea: old phones shouldn't end up abandoned in a drawer. Millions of devices with capable processors are forgotten because they no longer receive updates. I wanted to give them a second life by turning them into personal AI servers.

I built this project alone, learning to code from scratch since April 2023. There's no company behind it, no investors, no marketing team. Just a Spanish developer who believes technology should be accessible to everyone.

If ClawMobil is useful to you, share it. Every person who discovers it is a win. And if you'd like to support development, a coffee always helps. ❤️
</details>

<details>
<summary>🇧🇷 Português</summary>

ClawMobil nasceu de uma ideia simples: celulares antigos não deveriam acabar esquecidos numa gaveta. Milhões de dispositivos com processadores capazes ficam abandonados porque não recebem mais atualizações. Eu quis dar a eles uma segunda vida, transformando-os em servidores pessoais de inteligência artificial.

Construí este projeto sozinho, aprendendo a programar do zero desde abril de 2023. Não há empresa por trás, nem investidores, nem equipe de marketing. Apenas um programador espanhol que acredita que a tecnologia deve ser acessível para todos.

Se ClawMobil for útil para você, compartilhe. Cada pessoa que descobre é uma vitória. E se quiser apoiar o desenvolvimento, um café sempre ajuda. ❤️
</details>

<details>
<summary>🇫🇷 Français</summary>

ClawMobil est né d'une idée simple : les vieux téléphones ne devraient pas finir oubliés dans un tiroir. Des millions d'appareils dotés de processeurs performants sont abandonnés parce qu'ils ne reçoivent plus de mises à jour. J'ai voulu leur donner une seconde vie en les transformant en serveurs d'intelligence artificielle personnels.

J'ai construit ce projet seul, en apprenant à programmer à partir de zéro depuis avril 2023. Il n'y a pas d'entreprise derrière, pas d'investisseurs, pas d'équipe marketing. Juste un développeur espagnol qui croit que la technologie doit être accessible à tous.

Si ClawMobil vous est utile, partagez-le. Chaque personne qui le découvre est une victoire. Et si vous souhaitez soutenir le développement, un café aide toujours. ❤️
</details>

<details>
<summary>🇩🇪 Deutsch</summary>

ClawMobil entstand aus einer einfachen Idee: Alte Handys sollten nicht vergessen in einer Schublade enden. Millionen von Geräten mit leistungsfähigen Prozessoren werden aufgegeben, weil sie keine Updates mehr erhalten. Ich wollte ihnen ein zweites Leben geben, indem ich sie in persönliche KI-Server verwandle.

Ich habe dieses Projekt alleine aufgebaut und seit April 2023 von Grund auf programmieren gelernt. Es gibt kein Unternehmen dahinter, keine Investoren, kein Marketing-Team. Nur ein spanischer Entwickler, der glaubt, dass Technologie für alle zugänglich sein sollte.

Wenn ClawMobil für dich nützlich ist, teile es. Jede Person, die es entdeckt, ist ein Gewinn. Und wenn du die Entwicklung unterstützen möchtest, hilft ein Kaffee immer. ❤️
</details>

<details>
<summary>🇮🇹 Italiano</summary>

ClawMobil è nato da un'idea semplice: i vecchi telefoni non dovrebbero finire dimenticati in un cassetto. Milioni di dispositivi con processori capaci vengono abbandonati perché non ricevono più aggiornamenti. Ho voluto dar loro una seconda vita trasformandoli in server di intelligenza artificiale personali.

Ho costruito questo progetto da solo, imparando a programmare da zero da aprile 2023. Non c'è un'azienda dietro, non ci sono investitori, non c'è un team di marketing. Solo un programmatore spagnolo che crede che la tecnologia debba essere accessibile a tutti.

Se ClawMobil ti è utile, condividilo. Ogni persona che lo scopre è una vittoria. E se vuoi sostenere lo sviluppo, un caffè aiuta sempre. ❤️
</details>

## 💥 Compártelo. Que se entere todo el mundo.

Un español está creando una app para que CUALQUIER móvil viejo se convierta en una IA privada. Sin big tech, sin suscripciones, sin datos en la nube. **Compártelo y haz que llegue a quien lo necesite.**

[𝕏 Twitter / X](https://twitter.com/intent/tweet?text=🦞%20ClawMobil%20—%20Convierte%20cualquier%20móvil%20viejo%20en%20un%20servidor%20de%20IA%20personal.%20Sin%20cloud,%20sin%20suscripciones,%20100%25%20local%20y%20gratuito.%20https://erbolamm.github.io/ClawMobil/%20%23ClawMobil%20@erbolamm) · [💼 LinkedIn](https://www.linkedin.com/sharing/share-offsite/?url=https://erbolamm.github.io/ClawMobil/) · [💬 WhatsApp](https://api.whatsapp.com/send?text=🦞%20ClawMobil%20—%20Convierte%20cualquier%20móvil%20viejo%20en%20un%20servidor%20de%20IA%20personal.%20https://erbolamm.github.io/ClawMobil/) · [✈️ Telegram](https://t.me/share/url?url=https://erbolamm.github.io/ClawMobil/&text=🦞%20ClawMobil%20—%20Tu%20móvil%20viejo,%20tu%20IA%20privada.) · [🟠 Reddit](https://reddit.com/submit?url=https://erbolamm.github.io/ClawMobil/&title=ClawMobil%20—%20Convierte%20cualquier%20móvil%20viejo%20en%20un%20servidor%20de%20IA%20personal) · [🔵 Facebook](https://www.facebook.com/sharer/sharer.php?u=https://erbolamm.github.io/ClawMobil/) · [🧵 Threads](https://threads.net/intent/post?text=🦞%20ClawMobil%20—%20Convierte%20cualquier%20móvil%20viejo%20en%20un%20servidor%20de%20IA%20personal.%20https://erbolamm.github.io/ClawMobil/) · [📧 Email](mailto:?subject=ClawMobil%20—%20Tu%20móvil%20viejo,%20tu%20IA%20privada&body=Mira%20este%20proyecto:%20https://erbolamm.github.io/ClawMobil/)

## 💖 Apoya el proyecto

Herramienta gratuita y open source. Si te ahorra tiempo, un café ayuda a mantener el desarrollo.

| Plataforma | Enlace |
| ----------- | -------- |
| PayPal | [paypal.me/erbolamm](https://www.paypal.com/paypalme/erbolamm) |
| Ko-fi | [ko-fi.com/C0C11TWR1K](https://ko-fi.com/C0C11TWR1K) |
| Twitch Tip | [streamelements.com/apliarte/tip](https://streamelements.com/apliarte/tip) |

🌐 [Sitio Oficial](https://erbolamm.github.io/ClawMobil/) · 📦 [GitHub](https://github.com/erbolamm/ClawMobil)

## Licencia

MIT — © 2026 ApliArte

## About

Convierte cualquier móvil Android viejo en un servidor de IA personal. Sin cloud, sin suscripciones, 100% local y gratuito.
