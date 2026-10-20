# C4ptur3-th3-Fl4g

**Plataforma:** TryHackMe  
**Dificultad:** Fácil  
**Categoría:** Criptografía / Esteganografía  
**Room:** https://tryhackme.com/room/c4ptur3th3fl4g

---

## Descripción

Este room no es un CTF tradicional de hacking — no hay máquina que atacar ni shell que obtener. El objetivo es aprender a reconocer y decodificar distintos tipos de encodings y técnicas de esteganografía que aparecen constantemente en CTFs reales. Desde binario hasta archivos escondidos dentro de imágenes, cada task te presenta un dato ofuscado y tienes que descifrar qué dice.

---

## Task 1 — Encodings

La Task 1 cubre 8 encodings distintos. La lógica es siempre la misma: identificar el tipo por su forma visual y aplicar la decodificación correcta.

| Encoding | Pista visual | Herramienta |
|---|---|---|
| Binario | Solo 0s y 1s en grupos de 8 | CyberChef - From Binary |
| Base32 | Mayúsculas + `======` al final | `base32 -d` |
| Base64 | Mayúsculas/minúsculas + `==` al final | `base64 -d` |
| Hexadecimal | Grupos de 2 chars 0-9/a-f | `xxd -r -p` |
| ROT13 | Texto casi legible, letras desplazadas | CyberChef - ROT13 |
| ROT47 | Símbolos y números también desplazados | CyberChef - ROT47 |
| Morse | Puntos y rayas | CyberChef - From Morse Code |
| Decimal | Números separados por espacios (32-126) | CyberChef - From Charcode |

Para los que se hacen en terminal, el patrón es simple:

```bash
echo "CADENA======" | base32 -d
echo "CADENA==" | base64 -d
echo "68 65 78" | xxd -r -p
# ROT13 — CyberChef
```

Ejemplo de Base32 en terminal y ROT47 en CyberChef:

![Decodificando Base32 en terminal](img/02-base32.png)

![Decodificando ROT47 en CyberChef](img/06-rot47.png)

---

### Multi-layer encoding

Acá se pone interesante. La cadena estaba codificada en múltiples capas apiladas. Fui probando hasta descubrir el orden correcto: **Base64 → Morse → Binario → ROT47 → Decimal**. Todo en una sola receta en CyberChef.

![Decodificando multi-layer en CyberChef](img/09-multilayer.png)

---

## Task 2 — Spectrograms

Me dieron un archivo `.WAV`. La clave acá es que el mensaje no está en el audio que escuchas sino en la **visualización del espectrograma** — una representación gráfica de las frecuencias del audio a lo largo del tiempo.

Usé [dcode.fr/spectral-analysis](https://www.dcode.fr/spectral-analysis) para visualizarlo y el texto apareció directamente en la imagen del espectrograma.

![Espectrograma mostrando el mensaje oculto](img/10-spectrogram.png)

---

## Task 3 — Steganography

Me dieron una imagen y tenía que extraer datos ocultos con **steghide**. Esta herramienta permite esconder archivos dentro de imágenes o audio usando el algoritmo LSB (Least Significant Bit). En Parrot OS tuve problemas de dependencias para instalar steghide, así que usé la herramienta online [futureboy.us/stegano/decinput.html](https://futureboy.us/stegano/decinput.html).

```bash
steghide extract -sf ARCHIVO.jpg
```

---

## Task 4 — Security through obscurity

Me dieron un archivo `meme_1559010886025.jpg`. A simple vista parece solo una imagen. Primero verifiqué con `file` que efectivamente era un JPEG:

```bash
file meme_1559010886025.jpg
```

![Comando file sobre el JPEG](img/12-file-command.png)

Intenté renombrarlo a `.zip` y descomprimirlo, pero falló. Entonces usé `strings` para extraer texto legible del binario:

```bash
strings meme_1559010886025.jpg | tail -20
```

Al final del output aparecieron el nombre del archivo PNG escondido dentro del JPEG y un mensaje.

![strings revelando el archivo oculto](img/13-strings.png)

La técnica se llama **file-in-file** o **polyglot**: un archivo válido que al mismo tiempo contiene otro archivo embebido. Es una forma de esteganografía sin cifrado — la ocultación depende de que nadie piense en buscar adentro.

---

## Herramientas utilizadas

| Herramienta | Uso |
|---|---|
| CyberChef | Decodificación de Binary, ROT13, ROT47, Morse, Decimal, multi-layer |
| Terminal (base32/base64/xxd) | Decodificación directa de Base32, Base64, Hex |
| `strings` | Extraer texto legible de binarios |
| `file` | Identificar tipo real de archivo |

---

## Conceptos clave

- **Encoding vs Cifrado**: encodings como Base64 o Hex no son cifrado — no usan clave y son reversibles públicamente. Son ofuscación, no seguridad.
- **Espectrograma**: representación visual de las frecuencias de un audio. Se puede usar para esconder texto en la forma de las ondas.
- **LSB Steganography**: modificar los bits menos significativos de los píxeles de una imagen para esconder datos sin cambio visual perceptible. Steghide usa esta técnica.
- **File-in-file**: un archivo puede contener los bytes de otro archivo embebido. `strings` y `binwalk` son las herramientas para detectarlo.

---

## Referencias

- [CyberChef](https://gchq.github.io/CyberChef)
- [dcode.fr - Spectral Analysis](https://www.dcode.fr/spectral-analysis)
- [FutureBoy Steganography](https://futureboy.us/stegano/decinput.html)
- [AperiSolve](https://www.aperisolve.com)