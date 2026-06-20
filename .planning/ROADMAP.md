# Roadmap: Amplic AI Learning Hub

## Overview

Transformar a Dharrell y Jose de principiantes a expertos en IA mediante una plataforma web interactiva con roadmap visual, catalogo de recursos curados, y tracking de progreso individual. La plataforma se construye en SvelteKit con Svelte Flow, localStorage para persistencia, y deploy en Vercel.

## Phases

**Phase Numbering:**
- Integer phases (1, 2, 3): Planned milestone work
- Decimal phases (2.1, 2.2): Urgent insertions (marked with INSERTED)

Decimal phases appear between their surrounding integers in numeric order.

- [ ] **Phase 1: Project Scaffold and Deploy** - SvelteKit project con Tailwind, deploy inicial en Vercel
- [ ] **Phase 2: Data Model and User Switching** - JSON de recursos, selector de perfil, localStorage
- [ ] **Phase 3: Resource Catalog** - Vista de recursos por area con checkboxes de completado
- [ ] **Phase 4: Progress Tracking** - Barras de progreso por area y dashboard de estadisticas
- [ ] **Phase 5: Curated Content - LLMs and Prompting** - Recursos curados para el area prioritaria
- [ ] **Phase 6: Curated Content - Deep Learning and CV** - Recursos curados para Deep Learning y Computer Vision
- [ ] **Phase 7: Visual Roadmap** - Mapa interactivo de nodos con Svelte Flow
- [ ] **Phase 8: Roadmap Interactivity** - Nodos con color por progreso y click-to-navigate
- [ ] **Phase 9: Polish and Responsive** - Responsive design, UX refinements, ruta recomendada visible

## Phase Details

### Phase 1: Project Scaffold and Deploy
**Goal**: La plataforma existe online y es accesible desde cualquier dispositivo
**Mode:** mvp
**Depends on**: Nothing (first phase)
**Requirements**: CORE-01
**Success Criteria** (what must be TRUE):
  1. Usuario puede abrir la URL de Vercel desde movil o desktop y ver la app
  2. El proyecto SvelteKit compila y despliega sin errores
  3. Tailwind CSS esta configurado y funcional
**Plans**: TBD
**UI hint**: yes

### Phase 2: Data Model and User Switching
**Goal**: Cada co-founder tiene su propio perfil con datos independientes persistidos
**Mode:** mvp
**Depends on**: Phase 1
**Requirements**: CORE-02, CORE-03, CORE-04
**Success Criteria** (what must be TRUE):
  1. Usuario puede seleccionar su perfil (Dharrell o Jose) con un toggle o dropdown
  2. El progreso de cada usuario se guarda en localStorage y sobrevive recargas del navegador
  3. Los datos de contenido se cargan desde archivos JSON estaticos sin backend
  4. Cambiar de perfil muestra el progreso del usuario seleccionado, no del otro
**Plans**: TBD
**UI hint**: yes

### Phase 3: Resource Catalog
**Goal**: Usuarios pueden explorar y marcar recursos organizados por area de IA
**Mode:** mvp
**Depends on**: Phase 2
**Requirements**: CAT-01, CAT-02, CAT-03, CAT-05
**Success Criteria** (what must be TRUE):
  1. Usuario puede ver recursos agrupados por area (LLMs/Prompting, Deep Learning, Computer Vision)
  2. Cada recurso muestra titulo, tipo, URL, duracion estimada, y nivel
  3. Usuario puede marcar/desmarcar un recurso como completado via checkbox
  4. Agregar un recurso requiere solo editar un archivo JSON y redesplegar
**Plans**: TBD
**UI hint**: yes

### Phase 4: Progress Tracking
**Goal**: Usuarios pueden ver su progreso cuantificado por area y en general
**Mode:** mvp
**Depends on**: Phase 3
**Requirements**: PROG-01, PROG-02, PROG-03, PROG-04
**Success Criteria** (what must be TRUE):
  1. Usuario puede ver una barra de progreso por cada area tematica con porcentaje
  2. Usuario puede ver un dashboard con total completados, porcentaje general, y desglose por area
  3. El progreso se recalcula automaticamente al marcar/desmarcar checkboxes
  4. Dharrell y Jose ven progreso completamente independiente al cambiar de perfil
**Plans**: TBD
**UI hint**: yes

### Phase 5: Curated Content - LLMs and Prompting
**Goal**: El area prioritaria del negocio tiene recursos curados de calidad
**Mode:** mvp
**Depends on**: Phase 3
**Requirements**: CONT-01, CONT-02, CAT-04
**Success Criteria** (what must be TRUE):
  1. Area LLMs/Prompting tiene recursos sobre Claude, GPT, prompt engineering, RAG, y agentes
  2. El curso de Anthropic aparece como recurso destacado
  3. Los recursos son actuales (2025-2026) y cubren de principiante a avanzado
**Plans**: TBD

### Phase 6: Curated Content - Deep Learning and CV
**Goal**: Las areas tecnicas tienen recursos curados con ruta de aprendizaje clara
**Mode:** mvp
**Depends on**: Phase 5
**Requirements**: CONT-03, CONT-04, CONT-05
**Success Criteria** (what must be TRUE):
  1. Area Deep Learning tiene recursos sobre redes neuronales, CNNs, y transformers
  2. Area Computer Vision tiene recursos sobre procesamiento de imagenes y deteccion de objetos
  3. Cada area tiene una ruta clara de principiante a avanzado
**Plans**: TBD

### Phase 7: Visual Roadmap
**Goal**: Usuarios pueden ver un mapa visual de su ruta de aprendizaje
**Mode:** mvp
**Depends on**: Phase 4
**Requirements**: MAP-01, MAP-04
**Success Criteria** (what must be TRUE):
  1. Usuario puede ver un mapa de nodos conectados mostrando areas de IA y sus dependencias
  2. El roadmap muestra la ruta recomendada de aprendizaje (fundamentos a avanzado)
  3. Svelte Flow renderiza el grafo correctamente en desktop
**Plans**: TBD
**UI hint**: yes

### Phase 8: Roadmap Interactivity
**Goal**: El mapa visual responde al progreso del usuario y permite navegacion
**Mode:** mvp
**Depends on**: Phase 7
**Requirements**: MAP-02, MAP-03
**Success Criteria** (what must be TRUE):
  1. Los nodos cambian de color segun progreso (sin empezar / en progreso / completado)
  2. Usuario puede hacer click en un nodo para ver los recursos de esa area
  3. El color de los nodos se actualiza en tiempo real al completar recursos
**Plans**: TBD
**UI hint**: yes

### Phase 9: Polish and Responsive
**Goal**: La plataforma es usable y atractiva en cualquier dispositivo
**Mode:** mvp
**Depends on**: Phase 8
**Requirements**: (cross-cutting polish for all requirements)
**Success Criteria** (what must be TRUE):
  1. La plataforma se ve bien y es funcional en movil, tablet, y desktop
  2. La navegacion entre secciones (catalogo, dashboard, roadmap) es clara e intuitiva
  3. El roadmap visual tiene fallback o adaptacion razonable en pantallas pequenas
**Plans**: TBD
**UI hint**: yes

## Progress

**Execution Order:**
Phases execute in numeric order: 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7 -> 8 -> 9

| Phase | Plans Complete | Status | Completed |
|-------|----------------|--------|-----------|
| 1. Project Scaffold and Deploy | 0/0 | Not started | - |
| 2. Data Model and User Switching | 0/0 | Not started | - |
| 3. Resource Catalog | 0/0 | Not started | - |
| 4. Progress Tracking | 0/0 | Not started | - |
| 5. Curated Content - LLMs and Prompting | 0/0 | Not started | - |
| 6. Curated Content - Deep Learning and CV | 0/0 | Not started | - |
| 7. Visual Roadmap | 0/0 | Not started | - |
| 8. Roadmap Interactivity | 0/0 | Not started | - |
| 9. Polish and Responsive | 0/0 | Not started | - |
