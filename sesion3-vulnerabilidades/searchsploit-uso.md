# 🗂️ Searchsploit (Exploit-DB local) - Sesión 3

`searchsploit` viene preinstalado en Kali y permite buscar exploits públicos sin salir a internet (usa una copia local de Exploit-DB).

---

## 🔹 Comandos básicos

| Comando | Qué hace |
|---|---|
| `searchsploit vsftpd` | Busca exploits relacionados a "vsftpd" |
| `searchsploit vsftpd 2.3.4` | Busca por producto + versión específica |
| `searchsploit -u` | Actualiza la base de datos local |
| `searchsploit -w <término>` | Devuelve además el link web a Exploit-DB |
| `searchsploit -x <ruta_exploit>` | Muestra el contenido del exploit encontrado |
| `searchsploit -m <ruta_exploit>` | Copia el exploit a tu directorio actual para usarlo |

## 🧪 Ejemplo de flujo completo

```bash
# 1. Buscar exploits para el servicio detectado en Nmap
searchsploit vsftpd 2.3.4
```

```
------------------------------------------------------- ---------------------------------
 Exploit Title                                          |  Path
------------------------------------------------------- ---------------------------------
vsftpd 2.3.4 - Backdoor Command Execution                | unix/remote/49757.py
------------------------------------------------------- ---------------------------------
```

```bash
# 2. Ver el contenido del exploit antes de ejecutarlo (SIEMPRE revisar antes de correr)
searchsploit -x unix/remote/49757.py

# 3. Copiarlo a tu carpeta de trabajo
searchsploit -m unix/remote/49757.py
```

> ⚠️ Nunca ejecutes un exploit descargado sin antes leer el código. En la Sesión 5 usaremos principalmente Metasploit, que valida y encapsula esto mejor que un script suelto.

## 🔹 Complemento: buscar en la web

Si `searchsploit` no encuentra nada localmente, consulta:
- https://www.exploit-db.com
- https://nvd.nist.gov (para el detalle oficial del CVE y su CVSS)

---

## ✅ Checklist de esta fase

- [ ] Ejecuté `searchsploit -u` antes de empezar (base de datos actualizada)
- [ ] Busqué exploit para cada servicio vulnerable identificado
- [ ] Leí el código del exploit antes de considerarlo para la Sesión 5
- [ ] Anoté el nombre/ruta del exploit en mi reporte de hallazgos
