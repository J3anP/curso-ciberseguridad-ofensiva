# 🛰️ Nmap Cheatsheet - Sesión 2

Referencia rápida de los escaneos que vamos a usar contra Metasploitable2 en el laboratorio.

---

## 🔹 Escaneos básicos

| Comando | Qué hace |
|---|---|
| `nmap <IP>` | Escaneo rápido de los 1000 puertos TCP más comunes |
| `nmap -p- <IP>` | Escanea **todos** los puertos (1-65535) |
| `nmap -p 22,80,445 <IP>` | Escanea solo los puertos indicados |
| `nmap -sn <IP/24>` | Descubrimiento de hosts vivos en una subred (sin escanear puertos) |

## 🔹 Tipos de escaneo

| Flag | Nombre | Notas |
|---|---|---|
| `-sS` | SYN scan ("sigiloso") | Requiere privilegios root, no completa el handshake TCP |
| `-sT` | TCP connect scan | Completa el handshake, más "ruidoso" pero no requiere root |
| `-sU` | UDP scan | Más lento, útil para servicios como DNS (53), SNMP (161) |

## 🔹 Detección de servicios y sistema operativo

| Comando | Qué hace |
|---|---|
| `nmap -sV <IP>` | Detecta versión de los servicios en cada puerto abierto |
| `nmap -O <IP>` | Intenta identificar el sistema operativo |
| `nmap -A <IP>` | Combina `-sV -O` + traceroute + scripts básicos (más lento, más completo) |

## 🔹 Scripts NSE (Nmap Scripting Engine)

| Comando | Qué hace |
|---|---|
| `nmap --script=default <IP>` | Corre los scripts por defecto (info básica no intrusiva) |
| `nmap --script=vuln <IP>` | Busca vulnerabilidades conocidas en los servicios detectados |
| `nmap -sV --script=smb-os-discovery <IP>` | Ejemplo de script específico: info del SO vía SMB |

## 🔹 Formato de salida

| Comando | Qué hace |
|---|---|
| `nmap -oN salida.txt <IP>` | Guarda la salida en texto plano |
| `nmap -oX salida.xml <IP>` | Guarda en XML (útil si luego se importa a otra herramienta) |

---

## 🧪 Ejemplo de flujo recomendado en el laboratorio

```bash
# 1. Descubrir hosts vivos en la red del lab
nmap -sn 192.168.56.0/24

# 2. Escaneo completo de puertos contra el objetivo
nmap -p- -T4 192.168.56.X

# 3. Escaneo detallado sobre los puertos encontrados
nmap -sV -sC -p 21,22,80,139,445,3306 192.168.56.X

# 4. Búsqueda de vulnerabilidades conocidas
nmap --script=vuln -p 21,445 192.168.56.X
```

> 💡 `-T4` acelera el escaneo (timing template). No usar `-T4`/`-T5` en redes que no controles: es más ruidoso y detectable.

## 📖 Interpretando la salida

```
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd 2.3.4
22/tcp   open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1
80/tcp   open  http        Apache httpd 2.2.8
139/tcp  open  netbios-ssn Samba smbd 3.X
445/tcp  open  netbios-ssn Samba smbd 3.X
```

- `vsftpd 2.3.4` → versión con backdoor conocido (CVE-2011-2523), buena candidata para la Sesión 5.
- `Samba 3.X` → revisar en Exploit-DB en la Sesión 3.
