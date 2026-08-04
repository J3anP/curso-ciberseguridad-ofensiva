# ⚔️ Curso de Ciberseguridad Ofensiva — Cheatsheets y Ejemplos

> Repositorio de referencia rápida con los comandos, herramientas y ejemplos usados en cada sesión práctica del curso. Pensado para consultarse durante los laboratorios, no como reemplazo de la guía teórica.

---

## 🗺️ Estructura del repositorio

```
curso-ciberseguridad-ofensiva/
├── sesion2-reconocimiento/
│   ├── README.md
│   ├── nmap-cheatsheet.md
│   ├── osint-comandos.md
│   └── assets/               ← aquí va la foto de la espada de esta sesión
├── sesion3-vulnerabilidades/
│   ├── README.md
│   ├── nmap-nse-vuln.md
│   ├── searchsploit-uso.md
│   └── assets/
├── sesion4-web/
│   ├── README.md
│   ├── sqlmap-cheatsheet.md
│   ├── burpsuite-config.md
│   ├── payloads-ejemplo.md
│   └── assets/
├── sesion5-explotacion/
│   ├── README.md
│   ├── metasploit-cheatsheet.md
│   ├── msfvenom-payloads.md
│   ├── privesc-checklist.md
│   └── assets/
└── README.md   ← estás aquí
```

> ℹ️ La Sesión 1 (fundamentos/legal/redes) y la Sesión 6 (CTF final/reporte) no tienen carpeta de cheatsheets: la primera es teórica y la última usa la [plantilla de reporte de vulnerabilidades](../) que ya se entregó aparte.

---

## 🗡️ El arma de cada sesión

Cada carpeta de sesión tiene su propia "espada" como identidad visual — súbela tú en la carpeta `assets/` de cada sesión con el nombre indicado.

| Sesión | Tema | Color de espada | Nombre de archivo sugerido |
|---|---|---|---|
| **Sesión 2** | Reconocimiento (OSINT + Nmap) | 🩷 Rosa | `sesion2-reconocimiento/assets/espada-rosa.jpg` |
| **Sesión 3** | Análisis de vulnerabilidades | 🟣 Púrpura | `sesion3-vulnerabilidades/assets/espada-purpura.jpg` |
| **Sesión 4** | Seguridad web (Burp/SQLi/XSS) | ⚫ Negro | `sesion4-web/assets/espada-negra.jpg` |
| **Sesión 5** | Explotación (Metasploit) | 🔴 Rojo | `sesion5-explotacion/assets/espada-roja.jpg` |

Cada `README.md` de sesión ya tiene el tag de imagen listo (`![Espada de la sesión](./assets/espada-XXXXX.jpg)`) — solo reemplaza el archivo con tu foto y el nombre exacto, y se va a ver automáticamente.

---

## ⚠️ Aviso

Todos los comandos y ejemplos de este repositorio están pensados exclusivamente para el entorno de laboratorio aislado del curso (Kali Linux + Metasploitable2 + DVWA / Juice Shop). No deben usarse contra sistemas sin autorización explícita por escrito.
