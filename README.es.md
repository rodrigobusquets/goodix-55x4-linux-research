# Investigación Goodix 55x4 para Linux

Investigación independiente sobre el sensor de huellas Goodix `27c6:55b4` y su compatibilidad con Linux y libfprint.

**Idioma:** [English](README.md) | Español

## Objetivo

Investigar el protocolo, la compatibilidad del firmware, el aprovisionamiento PSK, la comunicación USB y la inicialización TLS de los sensores Goodix.

El objetivo es documentar hallazgos reproducibles, desarrollar mejoras probadas sin hardware y aportar evidencia técnica a la comunidad Linux.

## Hardware investigado

| Propiedad | Valor |
|---|---|
| ID USB | `27c6:55b4` |
| Firmware | `GF3268_RTSEC_APP_10024` |
| Controlador | Goodix TLS para libfprint |
| Plataforma | Linux |

## Hallazgos actuales

- El sensor responde al comando de lectura PSK (`0xE4`).
- El hash PSK obtenido no coincide con el esperado.
- El controlador original intenta aprovisionar automáticamente una PSK mediante `0xE0` cuando detecta una discrepancia.
- Durante una sesión de diagnóstico modificada, el intento de aprovisionamiento expiró después de cinco segundos.
- Una lectura posterior del hash PSK tampoco coincidió con el valor esperado.
- La implementación de diagnóstico detuvo la activación en lugar de reintentar la escritura.

Estas observaciones no demuestran si existe incompatibilidad del firmware, un fallo de aprovisionamiento por otra causa o algún cambio de estado del dispositivo.

## Trabajo experimental

Se implementó localmente el comando `0xF6` GET_IAP_VERSION.

La implementación incluye:

- Codificación de la solicitud.
- Lectura y validación de la respuesta.
- Pruebas offline de paquetes y respuestas.

**Todavía no se ha ejecutado contra hardware físico.**

Consulta el [parche experimental IAP](patches/README.md).

## Principios de investigación

- No ejecutar escrituras de hardware no documentadas.
- No flashear firmware.
- No realizar aprovisionamiento PSK automático durante diagnósticos.
- Priorizar pruebas offline antes de probar hardware.
- Diferenciar claramente observaciones confirmadas e hipótesis.
- Preservar la autoría y las licencias originales.

## Estructura

- `docs/` — Documentación técnica.
- `diagnostics/` — Evidencia diagnóstica sanitizada.
- `patches/` — Modificaciones experimentales.

## Relación con el proyecto original

Esta investigación parte del controlador Goodix TLS de:

[GuNanOvO/goodix-55x4-linux](https://github.com/GuNanOvO/goodix-55x4-linux)

Este repositorio es un proyecto independiente, no una iniciativa oficial del proyecto original.

## Licencia

Las modificaciones de código derivadas de código LGPL-2.1-or-later siguen sujetas a los términos aplicables de LGPL.

Se conservan los avisos de copyright originales.

La documentación de investigación original se distribuye bajo CC BY 4.0.
