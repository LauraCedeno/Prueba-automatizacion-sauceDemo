# Casos de Prueba – MakersPay

## Iniciar sesión
| ID       | Título | Tipo | Precondición | Pasos | Datos | Esperado |
|----------|---|---|---|---|---|---|
| 01 | Login válido | Funcional | App abierta | Ingresar usuario y contraseña válidos y enviar | user válido / pass válido | Acceso al dashboard con saldo visible |
| 02 | Contraseña incorrecta | Negativa | App abierta | Ingresar user válido y pass inválido | user válido / pass inválido | Mensaje “Credenciales inválidas”, no hay sesión |
| 03 | Campos vacíos | Negativa | App abierta | Enviar con user y pass vacíos | — | Mensajes “El usuario es requerido”, “La contraseña es requerida” |
| 04 | Campos con espacios | Negativa | App abierta | Ingresar “ usuario ” y “ pass ” (con espacios) | user/pass válidos con espacios | App recorta espacios o muestra mensaje claro |
| 05 | Bloqueo por intentos fallidos | Seguridad | App abierta | 5 intentos fallidos seguidos | user válido / pass incorrecto | Cuenta bloqueada o captcha; mensaje claro |

## Ver saldo
| ID | Título | Tipo | Precondición | Pasos | Datos | Esperado |
|---|---|---|---|---|---|---|
| 01 | Saldo visible al ingresar | Funcional | Usuario logueado | Ir a dashboard | — | Saldo renderizado sin errores |
| 02 | Formato de moneda COP | UX | Usuario logueado | Ver saldo | 0; 5,000; 1,000,000 | Formato $ x.xxx.xxx COP, sin decimales (según regla) |
| 03 | Actualiza tras envío exitoso | Integración | Usuario con saldo suficiente | Enviar dinero y volver al dashboard | 10,000 | Saldo disminuye en 10,000 |

## Enviar dinero
| ID | Título | Tipo | Precondición | Pasos | Datos | Esperado |
|----|---|------|--------------|-------|-------|----------|
| 01 | Envío mínimo permitido | Funcional | Usuario A saldo 1,000,000; dest C | Enviar dinero | 5,000 COP a 3022222222 | Éxito; descuenta A; acredita C; historial en ambos |
| 02 | Monto < mínimo | Negativa | Igual | Enviar dinero | 4,999 COP | Error “El monto mínimo es 5000 COP”; saldos sin cambio |
| 03 | Máximo permitido | Límite | Usuario A con saldo suficiente | Enviar dinero | 2,000,000 COP | Éxito |
| 04 | > Máximo | Límite/Negativa | Igual | Enviar dinero | 2,000,001 COP | Error “El monto máximo es 2000000 COP” |
| 05 | Fondos insuficientes | Negativa | Usuario B saldo 10,000 | Enviar dinero | 20,000 COP | Error “Fondos insuficientes” |
| 06 | Autotransferencia | Negativa | Usuario A | Enviar a su propio teléfono | 5,000 COP | Error “No se puede enviar a su propio teléfono” |
