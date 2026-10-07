# LANOPS · motor

Motor de evaluación de LANOPS, plataforma de empleo a la medida para Gipuzkoa: lee el CV, lo compara con cada vacante y emite un certificado verificable de congruencia.

Fork de career-ops (https://github.com/career-ops-hq/career-ops), licencia MIT. Se conserva el archivo LICENSE original y la autoría de sus autores. Los prompts de `modes/` son la fuente de verdad que usa n8n; cualquier cambio sube la versión de rúbrica.

## LANOPS en local

Si no quieres subir tu CV a ninguna plataforma, puedes correr el mismo motor en tu ordenador. Es la misma rúbrica que usa la web de LANOPS (cinco dimensiones, nota de 1 a 5), pero todo se queda en una carpeta tuya: tu CV, las ofertas y tu registro de candidaturas.

**Qué hace:** pegas una oferta (de la web de una empresa, de Lanbide o de donde sea) y te devuelve un informe de encaje con tu CV, qué te falta y si merece la pena postular. También puede revisar las páginas de empleo de una lista de empresas.

**Qué no hace:** no envía candidaturas por ti ni emite el certificado verificable; eso solo lo hace la web, porque necesita el registro de LANOPS para que la empresa pueda comprobarlo.

### Qué necesitas
- [Node.js](https://nodejs.org) 18 o superior y [Git](https://git-scm.com).
- Un asistente de IA de terminal: Claude Code, Codex, Gemini CLI u OpenCode.
- Si no quieres que tu CV salga de tu equipo ni pagar nada: un modelo local con [Ollama](https://ollama.com) (`node ollama-eval.mjs --file oferta.txt`; ver `docs/RUNNING_ON_A_BUDGET.md`). Con un asistente en la nube, tu CV no pasa por LANOPS, pero sí por el proveedor de IA que uses.

### Pasos
```bash
git clone https://github.com/LanopsDMM/motor.git lanops-local
cd lanops-local
npm install
npm run doctor          # comprueba que todo está instalado
cp templates/portals.gipuzkoa.yml portals.yml  # 24 empresas de Gipuzkoa con página de empleo
```
1. Crea `cv.md` en la carpeta con tu CV en texto. Sin DNI, fecha de nacimiento ni dirección: no hacen falta.
2. Abre tu asistente en esa carpeta (por ejemplo, `claude`) y pídele en castellano que adapte el sistema a ti: «Actualiza mi perfil con este CV», «Busco puestos de recién graduado en Gipuzkoa».
3. Para revisar las páginas de empleo de las empresas de Gipuzkoa que ya trae `portals.yml`, pídele «Haz un escaneo» (modo `scan`). La lista sale de https://github.com/LanopsDMM/lanops/blob/main/data/empresas.csv; puedes añadir o quitar empresas pidiéndoselo al asistente.
4. Pega el enlace o el texto de una oferta y te devuelve la evaluación. Las ofertas de Lanbide (Open Data Euskadi, CC BY) también sirven.

La IA evalúa; tú decides. Nada se envía sin tu clic.

Guía completa (en castellano, del proyecto original): [README.es.md](README.es.md).
