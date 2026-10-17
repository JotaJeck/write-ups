# Ciberseguridad — Write-ups

Documentación de salas de TryHackMe y otros CTFs que voy resolviendo,
con foco en reconocimiento, explotación y escalada de privilegios.


## Metodología

Cada write-up sigue una estructura consistente:

1. **Reconocimiento** — escaneo de puertos y servicios
2. **Enumeración** — descubrimiento de rutas, tecnologías y datos
3. **Explotación / Foothold** — acceso inicial
4. **Escalada de privilegios** — de usuario a root/admin
5. **Lecciones aprendidas**

## Write-ups

### TryHackMe

| Sala | Dificultad | Técnicas |
|------|-----------|----------|
| [Easy Peasy](tryhackme/easy/easy-peasy/) | Fácil | Nmap, Gobuster, hashes, esteganografía, cron privesc |
| [Simple CTF](tryhackme/easy/simple-ctf/) | Fácil | Nmap, Gobuster, SQLi CVE-2019-9053, sudo vim privesc |
| [Bounty Hacker](tryhackme/easy/bounty-hacker/) | Fácil | Nmap, FTP anónimo, Hydra, sudo tar privesc |

## Herramientas

Nmap, Gobuster, curl, CyberChef, John the Ripper, steghide, SSH,
Python 3, ftp, Hydra