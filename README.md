# EGB - Técnicas Digitales III

Proyecto correspondiente a la Evaluación Globalizadora B (EGB) de Técnicas Digitales III.

La EGB está implementada sobre una Raspberry Pi 4 con Linux y se comunica con la EGA mediante UART.

## Arquitectura general

La comunicación sigue esta estructura:

Aplicación de usuario  
↓  
`/dev/egalink`  
↓  
Driver de kernel `ega_link`  
↓  
`serdev`  
↓  
UART3  
↓  
EGA / ESP32-S3

El driver de Linux se encarga únicamente del transporte de datos. La interpretación de comandos como `GET POSITION`, `SET ANGLE`, `GET STATUS`, etc. se realiza en la EGA.

## Estructura del proyecto

```text
ega_egb/
├── driver/
│   ├── ega_link.c
│   ├── ega-link-overlay.dts
│   └── Makefile
│
├── console/
│   └── ega_ctl.c
│
├── web/
│   ├── server.py
│   └── index.html
│
├── config/
│   ├── 99-egalink.rules
│   ├── ega-web.service
│   └── modules-load-ega_link.conf
│
├── docs/
│   ├── Manual_usuario_EGB.pdf
│   └── Manual_usuario_EGB.md
│
├── .gitignore
└── README.md