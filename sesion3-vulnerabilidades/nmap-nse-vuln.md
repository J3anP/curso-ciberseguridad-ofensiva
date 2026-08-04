# 🩻 Detección de Vulnerabilidades - Sesión 3

---

## 🔹 Categorías de scripts relevantes

| Categoría | Uso |
|---|---|
| `vuln` | Busca vulnerabilidades conocidas (CVE) en los servicios detectados |
| `safe` | Scripts que no arriesgan afectar el servicio (buenos para producción) |
| `intrusive` | Scripts más agresivos, solo en entornos de laboratorio autorizados |

## 🔹 Comandos básicos

```bash
# Escaneo de vulnerabilidades general
nmap --script=vuln <IP>

# Combinar detección de versión + scripts default + vuln
nmap -sV --script=default,vuln <IP>

# Vulnerabilidad específica de SMB (ej. MS17-010 / EternalBlue)
nmap --script=smb-vuln-ms17-010 -p 445 <IP>

# Vulnerabilidades específicas de un servicio HTTP
nmap --script=http-vuln* -p 80 <IP>
```

## 🔹 Scripts útiles por servicio

| Servicio | Script sugerido |
|---|---|
| FTP | `ftp-vuln-cve2010-4221` |
| SMB | `smb-vuln-ms17-010`, `smb-vuln-cve-2017-7494` |
| HTTP | `http-vuln-cve*`, `http-shellshock` |
| SSL/TLS | `ssl-heartbleed`, `ssl-poodle` |

## 📖 Ejemplo de salida a interpretar

```
PORT    STATE SERVICE
445/tcp open  microsoft-ds
| smb-vuln-ms17-010:
|   VULNERABLE:
|   Remote Code Execution vulnerability in Microsoft SMBv1 servers (ms17-010)
|     State: VULNERABLE
|     IDs:  CVE:2017-0143
```

➡️ Con este resultado, el siguiente paso es documentar el CVE en el reporte y buscarlo en `searchsploit` (ver `searchsploit-uso.md`).

---

## ✅ Checklist de esta fase

- [ ] Corrí `--script=vuln` sobre todos los puertos abiertos relevantes
- [ ] Identifiqué al menos un CVE por servicio vulnerable
- [ ] Anoté el puntaje CVSS de cada CVE encontrado
- [ ] Prioricé la lista de hallazgos por severidad
