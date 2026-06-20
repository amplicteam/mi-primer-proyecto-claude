# Requirements — Amplic AI Learning Hub

## v1 Requirements

### Core Platform (CORE)

- [ ] **CORE-01**: Usuario puede acceder a la plataforma desde cualquier dispositivo via URL (deploy en Vercel)
- [ ] **CORE-02**: Usuario puede seleccionar su perfil (Dharrell o Jose) con un toggle/dropdown simple
- [ ] **CORE-03**: El progreso de cada usuario se persiste en localStorage del navegador
- [ ] **CORE-04**: La plataforma funciona sin backend — datos de contenido en archivos JSON estáticos

### Catálogo de Recursos (CAT)

- [ ] **CAT-01**: Usuario puede ver recursos organizados por área de IA (LLMs/Prompting, Deep Learning, Computer Vision)
- [ ] **CAT-02**: Cada recurso muestra: título, tipo (video/curso/doc), URL, duración estimada, nivel (principiante/intermedio/avanzado)
- [ ] **CAT-03**: Usuario puede marcar un recurso como completado via checkbox
- [ ] **CAT-04**: El catálogo incluye el curso de Anthropic como recurso destacado
- [ ] **CAT-05**: Los recursos se pueden agregar/modificar editando un archivo JSON (sin necesidad de admin UI)

### Progreso y Dashboard (PROG)

- [ ] **PROG-01**: Usuario puede ver una barra de progreso por cada área temática (% de recursos completados)
- [ ] **PROG-02**: Usuario puede ver un dashboard con estadísticas generales (total completados, % general, recursos por área)
- [ ] **PROG-03**: El progreso se calcula automáticamente basado en los checkboxes marcados
- [ ] **PROG-04**: Cada usuario (Dharrell/Jose) tiene su progreso completamente independiente

### Roadmap Visual (MAP)

- [ ] **MAP-01**: Usuario puede ver un mapa visual de nodos conectados que muestra las áreas de IA y sus dependencias
- [ ] **MAP-02**: Los nodos cambian de color según el progreso del usuario (sin empezar / en progreso / completado)
- [ ] **MAP-03**: Usuario puede hacer click en un nodo para ver los recursos de esa área
- [ ] **MAP-04**: El roadmap muestra la ruta recomendada de aprendizaje (de fundamentos a avanzado)

### Contenido Curado (CONT)

- [ ] **CONT-01**: La plataforma incluye recursos curados y actuales (2025-2026) para cada área de IA
- [ ] **CONT-02**: Área LLMs/Prompting: recursos sobre Claude, GPT, prompt engineering, RAG, agentes
- [ ] **CONT-03**: Área Deep Learning: recursos sobre redes neuronales, CNNs, transformers
- [ ] **CONT-04**: Área Computer Vision: recursos sobre procesamiento de imágenes, detección de objetos
- [ ] **CONT-05**: Cada área tiene una ruta clara de principiante a avanzado

## v2 Requirements (Deferred)

- [ ] Sincronización cross-device (Supabase o similar)
- [ ] Streak/racha de días consecutivos estudiando
- [ ] Estimación de tiempo restante por área
- [ ] Vista lado a lado del progreso Dharrell vs Jose
- [ ] Notas personales por recurso
- [ ] Filtros avanzados (por tipo, nivel, duración)

## Out of Scope

- Autenticación compleja (OAuth, email/password) — solo 2 usuarios fijos
- Gamificación (badges, leaderboards, puntos) — puede desmotivar en equipo pequeño
- Panel de administración — recursos se editan en JSON
- Integración directa con APIs de YouTube — link directo es suficiente
- App móvil nativa — web responsive cubre el caso
- Base de datos en v1 — localStorage es suficiente para 2 usuarios

## Traceability

| REQ-ID | Phase | Status |
|--------|-------|--------|
| (filled by roadmap) | | |

---
*19 requirements | 6 deferred | 6 exclusions*
