# Amplic AI Learning Hub

## What This Is

Una plataforma web interactiva estilo "curso" que funciona como roadmap de aprendizaje de Inteligencia Artificial para los co-founders de Amplic (Dharrell y Jose). Cada uno tiene su propio perfil con tracking de progreso individual. El objetivo final: dominar IA para vender servicios y productos de IA a empresas bajo la marca Amplic.

## Core Value

**Aprendizaje estructurado y trackeable de IA para dos personas**, con rutas claras de principiante a avanzado, recursos curados, y visibilidad del progreso de cada co-founder.

## Context

- **Marca:** Amplic — empresa de servicios y productos de IA para empresas
- **Usuarios:** Dharrell y Jose (co-founders)
- **Nivel actual:** Principiante-intermedio. Conocimientos generales pero sin dominio de conceptos como ML, redes neuronales, etc.
- **Motivación:** Necesitan dominar IA para poder vender servicios reales a empresas. No es hobby, es el core del negocio.
- **Fuentes de aprendizaje actuales:** YouTube (playlist curada), cursos online (Anthropic, etc.), documentación oficial, contenido de Instagram
- **Playlist de referencia:** https://www.youtube.com/playlist?list=PLn808TF66cpSrxN0W2ePmrm7E9iRzZ-eT
- **Deploy:** Online (Vercel/Netlify), accesible desde cualquier dispositivo

## Areas de IA (Prioridad)

1. **LLMs y Prompting** — Claude, GPT, prompt engineering, RAG, agentes (prioridad máxima por el negocio)
2. **Deep Learning** — Redes neuronales, CNNs, transformers
3. **Computer Vision** — Procesamiento de imágenes, detección de objetos
4. **Fundamentos ML** — Se cubre como base transversal dentro de las otras áreas

## Features de Tracking

- Checkboxes por recurso individual (video, curso, doc)
- Barra de progreso por área temática (% completado)
- Roadmap visual tipo mapa con nodos conectados
- Dashboard con estadísticas (horas, racha, progreso general)
- **Progreso individual por usuario** (Dharrell y Jose)

## Tech Stack

A definir por investigación — criterio: lo más práctico para deploy rápido online, con persistencia de datos de progreso por usuario.

## Requirements

### Validated

(None yet — ship to validate)

### Active

- [ ] Plataforma web desplegada online accesible desde cualquier dispositivo
- [ ] Sistema de 2 perfiles (Dharrell y Jose) con progreso independiente
- [ ] Roadmap visual de áreas de IA con rutas de aprendizaje
- [ ] Catálogo de recursos por área (videos, cursos, docs) con checkboxes
- [ ] Barra de progreso por área temática
- [ ] Dashboard con estadísticas de progreso
- [ ] Contenido curado de mejores recursos actuales (2025-2026)
- [ ] Incluir curso de Anthropic como recurso
- [ ] Sistema actualizable (agregar/quitar recursos fácilmente)

### Out of Scope

- Registro público / autenticación compleja — solo 2 usuarios fijos
- Gamificación avanzada (badges, leaderboards)
- Integración directa con APIs de YouTube/plataformas
- App móvil nativa — la web responsive es suficiente

## Key Decisions

| Decision | Rationale | Outcome |
|----------|-----------|---------|
| 2 usuarios fijos, sin auth complejo | Solo Dharrell y Jose usan la plataforma | Pending |
| Priorizar LLMs/Prompting primero | Es lo más cercano al negocio de Amplic | Pending |
| Deploy online | Acceso desde cualquier dispositivo | Pending |
| Recursos curados manualmente | Calidad sobre cantidad | Pending |

## Evolution

This document evolves at phase transitions and milestone boundaries.

**After each phase transition** (via `/gsd-transition`):
1. Requirements invalidated? → Move to Out of Scope with reason
2. Requirements validated? → Move to Validated with phase reference
3. New requirements emerged? → Add to Active
4. Decisions to log? → Add to Key Decisions
5. "What This Is" still accurate? → Update if drifted

**After each milestone** (via `/gsd:complete-milestone`):
1. Full review of all sections
2. Core Value check — still the right priority?
3. Audit Out of Scope — reasons still valid?
4. Update Context with current state

---
*Last updated: 2026-06-20 after initialization*
