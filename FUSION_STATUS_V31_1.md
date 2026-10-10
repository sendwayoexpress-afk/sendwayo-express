# SENDWAYO EXPRESS — Fusión Punto A + Punto B (V31.1)

## Estado real de entrega
**Rama de revisión; todavía no publicada en producción.** No se ha cambiado `main`, el Hosting activo ni los balances.

- Proyecto Firebase de destino: `sendwayo-express-app-101`.
- Repositorio de despliegue preparado: `sendwayoexpress-afk/sendwayo-express`.
- Rama: `fusion-a-b-v31-20261010`.
- PR del Punto A: https://github.com/sendwayoexpress-afk/sendwayo-express/pull/2
- PR complementario de revisión del Punto B: https://github.com/sendwayo-oficial/sendwayo-express/pull/17

## Incluido en esta rama
- Candidato V31.1 en `public/index.html`, configurado para inicializar Firebase desde el dominio del proyecto 101.
- Funciones de servidor bajo `backend/functions`, reglas e índices de Firestore.
- `.firebaserc` y `firebase.json` que apuntan explícitamente al proyecto 101.
- Workflows de validación y despliegue de vista previa/producción. Producción sólo se activa al integrar en `main`; requiere credencial de despliegue de Firebase.
- Saldos separados RD$/DOP y HTG/GDES, sin sumar balances durante la fusión ni crear balances o comisiones personales de agentes.
- Importador deduplicado que prioriza Punto A, completa campos faltantes de Punto B y deja balances ambiguos para revisión. No se ha ejecutado ninguna importación ni se han cambiado balances.

## Validación automática
- Pruebas de dominio: 16/16 pasan en la última versión validada de la rama de fusión.
- Sintaxis del backend: validada.
- Contrato cliente/servidor: las llamadas a funciones configuradas tienen exports correspondientes.
- Los workflows de validación están configurados para probar la sintaxis de los scripts HTML y el backend en cada actualización.

Estas son pruebas automatizadas de código y lógica; **no equivalen a una prueba de inicio de sesión, sincronización y transacciones contra el Firebase en vivo**.

## Bloqueos de publicación confirmados
1. La vista previa de Firebase se omitió porque el secreto de GitHub Actions `FIREBASE_TOKEN` no está configurado en el repositorio del Punto A. El workflow no publicó nada.
2. No se pudo inspeccionar desde esta sesión el contenido actual servido por el Hosting 101, ni confirmar sus cuentas de Authentication, reglas o colecciones reales. El candidato no debe sustituirse en producción hasta comprobar esos puntos.
3. Las cuentas antiguas y sus balances requieren exportación/importación y conciliación. El importador no inventa saldos, no suma las dos fuentes y nunca crea billeteras de agentes.
4. El despliegue del backend usa Cloud Functions for Firebase, que requiere el plan Blaze para desplegar funciones. Si el proyecto está en Spark, la parte de servidor no se desplegará desde Firebase sin resolver ese requisito.

## Próximo paso técnico
Configurar una credencial de despliegue de Firebase de forma segura en los secretos del repositorio (no compartirla por el chat), ejecutar la vista previa, verificar Authentication y Firestore del proyecto 101, y probar administrador/remitente/agente con cuentas autorizadas antes de integrar el PR en `main`.
