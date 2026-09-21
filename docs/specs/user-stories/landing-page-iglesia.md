# Landing Page pública para la Iglesia

**Como** administrador/webmaster voluntario de la iglesia (programador, no diseñador)
**Quiero** crear y publicar una landing page pública de bajo costo (idealmente gratuita) con información de la iglesia, imágenes en carrusel, y las distintas actividades (calendario, reuniones, mesa kids, jóvenes, mujeres, eventos, prédicas, donaciones), con un pipeline CI/CD desde GitHub que permita iterar fácilmente
**Para** poder mostrarle una versión de prueba a la iglesia, validar si les gusta la propuesta, y luego ir agregando funcionalidades (backoffice con contraseña, pasarela de pago para donaciones) de forma incremental sin comprometer presupuesto desde el inicio

**Criterios de aceptación:**
- [ ] Existe una decisión documentada sobre el framework a usar (React, Next.js o Astro) y por qué, considerando que el sitio es mayormente contenido estático/informativo
- [ ] Existe una recomendación de "skills" o buenas prácticas a seguir según el framework/lenguaje elegido
- [ ] Existe una guía o referencias de diseño (ejemplos de landing pages de iglesias) para que el usuario (no diseñador) pueda dar contexto visual
- [ ] El sitio cuenta con un carrusel de imágenes (fotos de eventos, logo, etc.) administrable sin necesidad de re-desplegar código manualmente
- [ ] Las imágenes se almacenan en un servicio gratuito o de muy bajo costo, con acceso público de lectura, consumible desde el frontend
- [ ] Existe un pipeline de CI/CD con GitHub Actions que despliega automáticamente el sitio ante cambios en la rama principal
- [ ] El sitio se publica en un hosting gratuito compatible con el framework elegido
- [ ] La landing incluye secciones/información sobre: calendario de actividades, reuniones generales, donaciones (informativo, sin pasarela de pago en esta primera fase), mesa de niños (mesa kids), reunión de jóvenes, reunión de mujeres, eventos, prédicas
- [ ] El calendario de actividades se implementa como una lista estática de eventos definida como contenido del sitio (ej. Markdown/JSON), actualizable vía commit/CI-CD, sin depender de servicios externos como Google Calendar
- [ ] Se genera un documento centralizado (roadmap/backlog de ideas) en formato Markdown dentro del propio repositorio (ej. `docs/roadmap.md`), versionado junto al código, donde se registran las funcionalidades futuras (backoffice administrable con contraseña, pasarela de pago para donaciones, etc.) para iterar feature por feature
- [ ] El backoffice de administración de contenido queda fuera de alcance de esta primera historia (se define como un proyecto/epic separado)
- [ ] El diseño es responsive (se ve bien en mobile y desktop)
