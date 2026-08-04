# 🕷️ Burp Suite — Configuración y Uso — Sesión 4

---

## 🔹 1. Configurar el proxy

1. Abre Burp Suite → pestaña **Proxy** → **Options**.
2. Verifica que el listener esté activo en `127.0.0.1:8080`.
3. En tu navegador, configura el proxy manual:
   - HTTP Proxy: `127.0.0.1`
   - Puerto: `8080`
4. Instala el certificado CA de Burp (necesario para interceptar HTTPS):
   - Visita `http://burp` en el navegador con el proxy activo → descarga el certificado → impórtalo como autoridad de confianza.

<!-- 📸 INSERTA AQUÍ (opcional): captura de la configuración del proxy en Burp Suite -->

## 🔹 2. Interceptar tráfico

| Pestaña | Uso |
|---|---|
| **Proxy → Intercept** | Pausa y permite modificar cada petición antes de enviarla |
| **Proxy → HTTP History** | Historial de todas las peticiones capturadas |
| **Repeater** | Reenviar y modificar manualmente una petición específica cuantas veces quieras |
| **Intruder** | Automatizar ataques de fuerza bruta o fuzzing sobre un parámetro |

## 🔹 3. Flujo típico de trabajo

```
1. Activa Intercept ON en la pestaña Proxy.
2. Navega en DVWA/Juice Shop y realiza una acción (ej. login, búsqueda).
3. La petición queda pausada en Burp.
4. Clic derecho → "Send to Repeater".
5. En Repeater, modifica el parámetro que quieras probar (ej. inyectar ' OR '1'='1).
6. Presiona "Send" y analiza la respuesta.
```

## 🔹 Ejemplo: modificar un parámetro en Repeater

Petición original:
```
GET /vulnerabilities/sqli/?id=1&Submit=Submit HTTP/1.1
Host: localhost
```

Petición modificada para probar SQLi:
```
GET /vulnerabilities/sqli/?id=1' OR '1'='1&Submit=Submit HTTP/1.1
Host: localhost
```

---

## ✅ Checklist de esta fase

- [ ] Proxy configurado y certificado CA instalado
- [ ] Al menos una petición interceptada y enviada a Repeater
- [ ] Un parámetro modificado exitosamente para observar cambio de comportamiento
- [ ] Captura de pantalla de la petición/respuesta guardada como evidencia
