# 🔍 OSINT Cheatsheet — Sesión 2

Recolección de información pública, sin interactuar directamente con el objetivo (reconocimiento pasivo).

---

## 🔹 Google Dorking

Operadores de búsqueda avanzada para encontrar archivos, paneles o información expuesta.

| Operador | Ejemplo | Qué encuentra |
|---|---|---|
| `site:` | `site:ejemplo.com` | Resultados solo de ese dominio |
| `filetype:` | `site:ejemplo.com filetype:pdf` | Archivos de un tipo específico |
| `inurl:` | `inurl:admin` | URLs que contienen esa palabra |
| `intitle:` | `intitle:"index of"` | Páginas cuyo título contiene esa frase (listados de directorios expuestos) |
| `"..."` | `"contraseña" filetype:xlsx` | Frase exacta dentro del documento |

```
# Ejemplos combinados
site:ejemplo.com inurl:login
site:ejemplo.com filetype:env
intitle:"index of" "backup"
```

## 🔹 Whois

```bash
whois ejemplo.com
```
Qué buscar en la salida: registrante, servidores DNS, fechas de registro/expiración, país.

## 🔹 theHarvester

Recolecta correos, subdominios y nombres asociados a un dominio desde fuentes públicas.

```bash
theHarvester -d ejemplo.com -b all
```

| Flag | Qué hace |
|---|---|
| `-d` | Dominio objetivo |
| `-b` | Fuente de búsqueda (`google`, `bing`, `all`, etc.) |
| `-l` | Límite de resultados |

```bash
# Ejemplo con límite de resultados
theHarvester -d ejemplo.com -b google -l 100
```

## 🔹 Shodan

Buscador de dispositivos y servicios expuestos en internet.

| Búsqueda en shodan.io | Qué encuentra |
|---|---|
| `apache country:"PE"` | Servidores Apache expuestos en Perú |
| `port:3389` | Dispositivos con RDP expuesto |
| `product:"MySQL"` | Bases de datos MySQL accesibles públicamente |

CLI (requiere API key gratuita):
```bash
shodan search apache country:PE
shodan host <IP>
```

---

## ✅ Checklist de reconocimiento pasivo

- [ ] Dominio y subdominios identificados (theHarvester)
- [ ] Correos/empleados públicos identificados
- [ ] Tecnologías expuestas vía Google Dorking
- [ ] Dispositivos/servicios expuestos en Shodan (si aplica)
- [ ] Info de registro del dominio (whois)
