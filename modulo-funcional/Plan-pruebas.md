# Plan de Pruebas – MakersPay (Módulo Funcional)

## Alcance
- Login, ver saldo, enviar dinero por número de celular.

## Reglas de negocio clave
- Min: 5.000 COP. Máx: 2.000.000 COP.
- No más del saldo disponible.
- Prohibido enviarse a sí mismo.
- Éxito: descuenta remitente, acredita destinatario, registra historial en ambos.
- Falla: mensaje claro, saldos intactos.

## Tipos y técnicas
- Funcional (positivo/negativo), Smoke, Regresión.
- Particiones de equivalencia, valores límite, tablas de decisión, BDD (Gherkin).

## Criterios de salida
- Escenarios críticos pasan (smoke).
- Sin bugs bloqueantes abiertos para el alcance.
