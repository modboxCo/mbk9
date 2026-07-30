# ⌨️ mbk9 Macropad

[![QMK Compatible](https://img.shields.io/badge/Firmware-QMK-blueviolet?style=for-the-badge)](https://qmk.fm/)
[![VIA Compatible](https://img.shields.io/badge/Config-VIA-red?style=for-the-badge)](https://usevia.app/)

El **mbk9** es un macropad de 9 teclas basado en el microcontrolador **Pro Micro RP2040**. Incluye iluminación RGB perimetral y dos encoders rotativos integrados en la propia PCB, totalmente personalizable mediante **VIA** para cambios en tiempo real o mediante **QMK** para modificaciones profundas de firmware.

---

## 🚀 Características
* **Controlador:** Pro Micro RP2040.
* **Layout:** 3x3 (9 teclas mecánicas).
* **Encoders:** 2 encoders rotativos integrados.
* **Iluminación:** RGB underglow (WS2812B, 9 LEDs) con múltiples efectos.
* **Software:** Compatible con VIA (mapeo dinámico sin necesidad de flashear).
* **Reset:** Bootmagic integrado en la tecla (1,0).
* **NKRO / Mouse keys / Extra keys** habilitados por firmware.

---

## 🛠️ Especificaciones Técnicas

### Matriz Fija (PCB)
Los pines de la matriz están integrados en la placa. Si deseas compilar tu propio firmware, asegúrate de mantener esta configuración en tu `keyboard.json`:

| Línea | Pin (Pro Micro RP2040) |
| :--- | :--- |
| **Col 0** | `GP6` |
| **Col 1** | `GP8` |
| **Col 2** | `GP14` |
| **Row 0** | `GP15` |
| **Row 1** | `GP26` |
| **Row 2** | `GP7` |

* **VID / PID:** `0x4D42` / `0x0095`
* **Diode Direction:** `COL2ROW`

### Periféricos Integrados

**RGB Underglow (WS2812B)**
* **Pin de datos:** `GP3`
* **Cantidad de LEDs:** 9
* Efectos incluidos: Breathing, Rainbow Mood, Rainbow Swirl, Snake, Knight, Christmas, Gradient, Twinkle, Alternating, RGB Test, entre otros. Configurables en tiempo real desde VIA (menú *Lighting → Underglow*).

**Encoders Rotativos**
* **Encoder 1:** Pines A `GP5` / B `GP4`
* **Encoder 2:** Pines A `GP27` / B `GP28`
* Resolución: 4 pasos por muesca.
* Mapeados por defecto a `KC_VOLU` / `KC_VOLD`, reasignables desde el `keymap.c` o mediante VIA (`ENCODER_MAP_ENABLE`).

---

## 💻 Configuración

### Acceso al Bootloader (Modo Flash)
El RP2040 puede entrar en modo bootloader (unidad de almacenamiento `RPI-RP2`) de varias formas:
1. **Bootmagic:** Mantén presionada la tecla en la posición **(1,0)** mientras conectas el USB.
2. **Botón BOOT físico:** Mantén presionado el botón BOOT de la Pro Micro RP2040 mientras conectas el USB.
3. **Keycode:** Si tienes `QK_BOOT` mapeado en tu capa, púlsalo para reiniciar directamente al bootloader.

### Personalización con VIA
1. Accede a [usevia.app](https://usevia.app/).
2. Importa el archivo de definición [`mbk9.json`](./via/mbk9.json) desde la carpeta `/via` de este repositorio.
3. Configura tus macros, capas y el color/efecto del RGB visualmente.

## ⚡ Flasheo del Firmware

Para cargar el firmware en tu mbk9, primero pon el teclado en **modo Bootloader** (ver sección anterior) y usa uno de los siguientes métodos:

### Método A: Arrastrar y soltar (RP2040 UF2)
1. Con el teclado en modo bootloader, aparecerá una unidad `RPI-RP2` en tu explorador de archivos.
2. Copia el archivo [`mbk9_v0.8.uf2`](./firmware/mbk9_v0.8.uf2) de la carpeta `/firmware` dentro de esa unidad.
3. El teclado se reiniciará automáticamente con el nuevo firmware.

### Método B: Consola QMK (CLI)
Si tienes el entorno de QMK instalado, usa el siguiente comando desde tu terminal:
```bash
qmk flash -kb mbk9 -km via
```

---

## 📁 Estructura del Repositorio
* `/src`: Código fuente base (`keyboard.json`, `keymaps/default`, `keymaps/via`).
* `/via`: Archivo JSON (`mbk9.json`) para compatibilidad con VIA.
* `/firmware`: Archivos `.uf2` compilados listos para usar.
* `/gerber`: Archivos de fabricación de la PCB (Gerber + taladros) y lista de materiales (BOM) — ver [`/gerber/README.md`](./gerber/README.md).
* `/3dmodel`: Modelos 3D del caso (top/bottom cover, plate, knobs, weight, keycap).
* `/images`: Diagramas y fotos del proyecto.

---

## ⚖️ Licencia y Documentación
Este proyecto es de código abierto (Open Source). Se permite la libre modificación y distribución del software para adaptar el hardware a necesidades específicas o añadir nuevas funcionalidades.

Para obtener información técnica detallada, guías de configuración avanzada y resolución de problemas, por favor consulta la **[Documentación oficial de QMK](https://docs.qmk.fm/)**.

---
