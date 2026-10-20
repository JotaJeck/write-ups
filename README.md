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
| [Bounty Hacker](tryhackme/easy/Bounty-Hacker/) | Fácil | Nmap, FTP anónimo, Hydra, sudo tar privesc |
| [Pickle Rick](tryhackme/easy/pickle-rick/) | Fácil | Nmap, código fuente HTML, RCE command injection, sudo ALL |
| [RootMe](tryhackme/easy/rootme/) | Fácil | Nmap -Pn, Gobuster, reverse shell PHP, bypass extensiones, SUID python privesc |
| [Kenobi](tryhackme/easy/kenobi/) | Fácil | Nmap, SMB, NFS, ProFTPD mod_copy CVE-2015-3306, PATH hijacking privesc |
| [C4ptur3-th3-Fl4g](tryhackme/easy/c4ptur3-th3-fl4g/) | Fácil | Encodings (Binary, Base32/64, Hex, ROT13/47, Morse, Decimal), espectrograma, steghide online, file-in-file |

## Herramientas

Nmap, Gobuster, curl, CyberChef, John the Ripper, steghide, SSH,
Python 3, ftp, Hydra, netcat, smbclient, searchsploit, strings