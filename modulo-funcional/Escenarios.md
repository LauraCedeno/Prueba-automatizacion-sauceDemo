# MakersPay – Escenarios

A continuación se documentan los escenarios funcionales clave de MakersPay. 

## Índice
- Login
- Ver saldo
- Enviar dinero

---

## Login
```gherkin

Feature: Inicio de sesión en MakersPay
  Como usuario de MakersPay
  Quiero iniciar sesión
  Para acceder a mi billetera

  Background:
    Given estoy en la página de inicio de sesión de MakersPay

  Scenario: Login exitoso con credenciales válidas
    When inicio sesión con usuario "LauraAndrade" y contraseña "Pass123"
    Then debo ver mi panel con el saldo

  Scenario: Login fallido con contraseña incorrecta
    When inicio sesión con usuario "LauraAndrade" y contraseña "12345"
    Then debo ver el error "Credenciales inválidas"

  Scenario: Validación de campos obligatorios
    When intento iniciar sesión sin usuario y sin contraseña
    Then debo ver el error "El usuario es requerido"
```

---

## Ver saldo
```gherkin

Feature: Ver saldo
  Como usuario de MakersPay
  Quiero ver el saldo de mi billetera
  Para conocer mis fondos disponibles

  Background:
    Given inicio sesión como "LauraAndrade"

  Scenario: El saldo se muestra en el panel
    When abro el panel de la billetera
    Then debo ver mi saldo actual
```

---

## Enviar dinero
```gherkin

Feature: Enviar dinero
  Como usuario de MakersPay
  Quiero enviar dinero a un usuario registrado por número de celular
  Para transferir fondos de forma segura

  Background:
    Given inicio sesión como "LauraAndrade" con saldo 1000000
    And existe el destinatario "MariaAndrade" con teléfono "3022222222"

  Scenario Outline: Transferencia exitosa dentro de los límites
    When envío <amount> COP al teléfono "3022222222"
    Then la transferencia debe ser exitosa
    And mi saldo debe disminuir en <amount>
    And el saldo del destinatario "MariaAndrade" debe incrementarse en <amount>
    And ambos historiales deben registrar la transferencia como "Exitosa"
    Examples:
      | amount  |
      | 5000    |
      | 2000000 |

  Scenario: Monto menor al mínimo
    When envío 4999 COP al teléfono "3022222222"
    Then debo ver el error "El monto mínimo es de 5000 COP"
    And mi saldo debe permanecer sin cambios

  Scenario: Monto mayor al máximo
    When envío 2000001 COP al teléfono "3022222222"
    Then debo ver el error "El monto máximo es 2000000 COP"
    And mi saldo debe permanecer sin cambios

  Scenario: Fondos insuficientes
    Given inicio sesión como "userB" con saldo 10000
    When envío 20000 COP al teléfono "3022222222"
    Then debo ver el error "Fondos insuficientes"
    And mi saldo debe permanecer sin cambios

  Scenario: No se permite transferirse a sí mismo
    When envío 5000 COP a mi propio teléfono
    Then debo ver el error "No se puede enviar a su propio teléfono"

  Scenario: Formato de teléfono inválido
    When envío 5000 COP al teléfono "12345"
    Then debo ver el error "Número de teléfono inválido"

  Scenario: Destinatario no encontrado
    When envío 5000 COP al teléfono "3099999999"
    Then debo ver el error "Destinataria no encontrada"
```
