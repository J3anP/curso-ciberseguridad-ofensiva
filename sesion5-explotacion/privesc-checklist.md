# 🪜 Escalada de Privilegios en Linux — Checklist Manual — Sesión 5

Una vez que tienes una shell con un usuario de bajos privilegios, estos son los primeros lugares donde buscar una vía hacia root.

---

## 🔹 1. Permisos sudo

```bash
sudo -l
```
Busca comandos que el usuario puede correr como root sin contraseña — muchos tienen "escapes" conocidos (consultar [GTFOBins](https://gtfobins.github.io/)).

## 🔹 2. Binarios con bit SUID activo

```bash
find / -perm -4000 -type f 2>/dev/null
```
Cualquier binario "no estándar" en esta lista (que no sea `passwd`, `sudo`, etc. típicos del sistema) es candidato a investigar en GTFOBins.

## 🔹 3. Cronjobs mal configurados

```bash
cat /etc/crontab
ls -la /etc/cron.d/
```
Si un cronjob ejecuta un script como root y ese script tiene permisos de escritura para tu usuario, puedes modificarlo para ejecutar tu propio código.

```bash
# Verificar permisos de un script de cron sospechoso
ls -la /ruta/al/script.sh
```

## 🔹 4. Información del sistema y kernel

```bash
uname -a
cat /etc/os-release
```
Con esta info puedes buscar exploits de escalada específicos del kernel en Exploit-DB (`searchsploit linux kernel <versión>`).

## 🔹 5. Variables de entorno y PATH

```bash
echo $PATH
```
Si un binario SUID llama a otro comando sin ruta absoluta y tu directorio está antes en el `PATH`, puedes hacer "PATH hijacking".

## 🔹 6. Archivos con contraseñas o credenciales

```bash
grep -ri "password" /etc/*.conf 2>/dev/null
find / -name "*.bak" -o -name "*config*" 2>/dev/null
history
cat ~/.bash_history
```

---

## 🧪 Flujo recomendado

```
1. sudo -l
2. find / -perm -4000 -type f 2>/dev/null
3. cat /etc/crontab
4. uname -a  →  buscar exploit de kernel si nada más funciona
5. Buscar archivos de configuración/backup con credenciales
```

## ✅ Checklist de esta fase

- [ ] Revisé `sudo -l`
- [ ] Busqué binarios SUID y los comparé contra GTFOBins
- [ ] Revisé cronjobs y sus permisos
- [ ] Documenté la vía de escalada exitosa (o los intentos, aunque no haya funcionado) en el reporte
