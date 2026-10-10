# SENDWAYO EXPRESS — Fusión A+B V31

## Objetivo de la rama
Esta rama prepara una fusión de revisión con el Punto A (proyecto Firebase `sendwayo-express-app-101`) como base visual y de acceso. Conserva del Punto B el comprobante, las sugerencias/autocompletado y las reglas de descuento, depósitos, acreditaciones y ajustes.

## Cambios incluidos
- `index.html`: candidato V31 con entrada Firebase Authentication, uso de Cloud Functions y consultas de datos/notificaciones en tiempo real.
- `functions/`: backend autenticado para perfiles, importación deduplicada, operaciones, aprobaciones/rechazos/No Coincide, reenvíos, ajustes en RD$/HTG, comisión, cuentas bancarias, paquetes, conciliación y beneficiarios.
- `firestore.rules`: denegación por defecto; los movimientos financieros se escriben solo mediante funciones de servidor.
- `firestore.indexes.json`: índices para consultas.
- `firebase.json` y `.firebaserc`: configuración de Hosting/Functions/Firestore destinada al proyecto existente.
- No hay un módulo de Capital en el candidato; se conservan los campos de saldo separados `balanceDOP` y `balanceHTG`. Los agentes no tienen balances ni comisión personal.

## Verificaciones locales
- Backend: `node --check functions/index.js`, `node --check functions/domain.js`.
- Unit tests: `node --test functions/test/domain.test.js` — 14/14.
- Frontend: 25 bloques de JavaScript inline comprobados sintácticamente.
- Contrato cliente/servidor: 21 funciones invocadas por el cliente y 21 exports callable coincidentes.
- Fusión de registros: prioridad Punto A, completa campos vacíos con Punto B, no suma balances, no resuelve automáticamente roles contradictorios ni asigna moneda no conocida.
  
## Importante: no es todavía producción
Esta rama no despliega nada por sí sola. No se han probado credenciales reales, Rules Emulator, multi-sesión, notificaciones en varios dispositivos, Storage ni flujos de extremo a extremo contra Firebase. No se importan usuarios/saldos automáticamente. Antes de integrar/publicar hay que revisar Firestore/Auth existentes y probar en Emulator Suite o proyecto de pruebas; la migración de balances exige revisión/aprobación explícita. No unir a `main` ni ejecutar `firebase deploy` hasta pasar esas pruebas.
