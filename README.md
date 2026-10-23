# Ciberseguridad — Write-ups

Documentación de salas de TryHackMe y otros CTFs que voy resolviendo,
con foco en reconocimiento, explotación, escalada de privilegios y
mitigaciones.

## Estructura de cada write-up

1. **Resumen** — qué había y cómo se llegó a root
2. **Habilidades demostradas**
3. **Reconocimiento y enumeración** — puertos, servicios, rutas
4. **Explotación / Acceso inicial**
5. **Escalada de privilegios**
6. **Lo que probé y no funcionó**
7. **Impacto** — qué podría hacer un atacante real
8. **Perspectiva defensiva** — cómo se corregiría
9. **Lecciones aprendidas**

## Write-ups

### TryHackMe

#### Fácil

| Sala | Dificultad | Técnicas |
|------|-----------|----------|
| [Easy Peasy](tryhackme/easy/easy-peasy/) | Fácil | Nmap `-p-`, Gobuster, Base62, hash GOST, steghide, SSH, cron privesc |
| [Simple CTF](tryhackme/easy/simple-ctf/) | Fácil | Nmap, Gobuster, SQLi CVE-2019-9053, sudo vim privesc |
| [Bounty Hacker](tryhackme/easy/Bounty-Hacker/) | Fácil | Nmap, FTP anónimo, Hydra, sudo tar privesc |
| [Pickle Rick](tryhackme/easy/pickle-rick/) | Fácil | Nmap, código fuente HTML, RCE panel de comandos, sudo ALL |
| [RootMe](tryhackme/easy/rootme/) | Fácil | Nmap -Pn, Gobuster, reverse shell PHP, bypass extensiones, SUID python privesc |
| [Kenobi](tryhackme/easy/kenobi/) | Fácil | Nmap, SMB, NFS, ProFTPD mod_copy CVE-2015-3306, PATH hijacking privesc |
| [C4ptur3-th3-Fl4g](tryhackme/easy/c4ptur3-th3-fl4g/) | Fácil | Encodings (Binary, Base32/64, Hex, ROT13/47, Morse, Decimal), espectrograma, esteganografía LSB (decodificador online), file-in-file |

#### Media

| Sala | Dificultad | Técnicas |
|------|-----------|----------|
| [Linux PrivEsc](tryhackme.com/room/linuxprivesc) | Media | sudo escapes, LD_PRELOAD/LD_LIBRARY_PATH, cron (script write/PATH/wildcard), SUID (MySQL UDF/exim CVE-2016-1531/SO injection/PATH hijacking/bash function export/PS4 debugging), credenciales expuestas, SSH key expuesta, NFS no_root_squash, Dirty COW CVE-2016-5195 |

## Herramientas

Nmap, Gobuster, curl, CyberChef, John the Ripper, steghide, SSH,
Python 3, ftp, Hydra, netcat, smbclient, searchsploit, strings, mount,
gcc, msfvenom, strace, linpeas, LinEnum