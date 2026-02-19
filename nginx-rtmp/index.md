# NF3 – Streaming de Vídeo amb Nginx-RTMP i Docker

**Mòdul:** M0375 – Serveis de Xarxa i Internet  
**Pràctica:** Streaming de Vídeo  
**Alumne:** Alex Marques  
**Tecnologia:** Nginx-RTMP + HLS + OBS Studio + Docker  

---

## Objectiu de la pràctica

L’objectiu d’aquesta pràctica és desplegar un **servidor de streaming de vídeo** utilitzant Nginx amb el mòdul RTMP dins d’un contenidor Docker, generar streams en format **HLS (HTTP Live Streaming)** i verificar la reproducció en directe mitjançant una pàgina web personalitzada.

També es treballa el concepte de **transcoding** per generar múltiples qualitats de vídeo adaptatives.

---

## Índex

1. Desplegament del servidor Nginx-RTMP  
2. Configuració del Streaming RTMP  
3. Generació i reproducció HLS  
4. Monitorització del servidor  
5. Proves i validació final  
6. Qüestions  
7. Reflexió final  

---

## 1) Desplegament del servidor Nginx-RTMP

### 1.1 Creació de l’estructura del projecte

Es crea l’estructura de directoris del projecte amb carpetes per a:

- Configuració (`config`)
- Fitxers web (`html`)
- Vídeos (`videos`)
- Fitxers HLS generats (`hls`)
- Fitxer `docker-compose.yml`

<img width="940" height="423" alt="image" src="https://github.com/user-attachments/assets/9b60ba7f-4c6f-43f5-861a-4bd5035c0269" />

---

### 1.2 Configuració del fitxer nginx.conf

Es configura el servidor Nginx amb:

- Servidor RTMP escoltant al port 1935
- Aplicació `live` per rebre el stream
- Generació automàtica de segments HLS
- Transcoding a múltiples qualitats (1080p, 720p, 480p)
- Servidor HTTP al port 8080 per servir el contingut web i els fitxers HLS

<img width="940" height="460" alt="image" src="https://github.com/user-attachments/assets/19cf7588-1d47-438b-a3d8-b2d67b8c800a" />

---

### 1.3 Configuració del docker-compose.yml

Es defineix el servei Nginx-RTMP amb:

- Ports 1935 (RTMP) i 8080 (HTTP)
- Volums per a configuració, web i HLS
- Xarxa bridge personalitzada
- Reinici automàtic del contenidor

<img width="940" height="573" alt="image" src="https://github.com/user-attachments/assets/551135f9-2730-4bf7-b2b5-11d6eb4636b8" />

---

### 1.4 Inici del servidor

S’inicia el contenidor i es comprova:

- Que està en execució
- Que no hi ha errors als logs

<img width="940" height="210" alt="image" src="https://github.com/user-attachments/assets/39d170c8-5aff-4661-a031-26816463cac8" />

<img width="940" height="356" alt="image" src="https://github.com/user-attachments/assets/5dd3a33b-a7d6-425c-9de3-f38994568c10" />

---

## 2) Configuració del Streaming RTMP

### 2.1 Configuració d’OBS Studio

Es configura OBS Studio amb:

- Servei personalitzat
- URL del servidor RTMP
- Clau d’emissió personalitzada

<img width="940" height="277" alt="image" src="https://github.com/user-attachments/assets/1c64be41-94c8-4be8-98a1-fb0adfeed69a" />

---

### 2.2 Emissió en directe amb el nom visible

S’afegeix una font de vídeo i un text amb el nom complet visible durant l’emissió.

Es verifica que el stream arriba correctament al servidor.

<img width="940" height="467" alt="image" src="https://github.com/user-attachments/assets/6548e8a5-a551-4002-bad1-c654d13846cb" />

---

## 3) Generació i reproducció HLS

### 3.1 Pàgina web personalitzada

Es crea una pàgina HTML que permet:

- Reproduir el stream HLS
- Visualitzar el nom personalitzat
- Accedir a les estadístiques del servidor

<img width="940" height="479" alt="image" src="https://github.com/user-attachments/assets/21ff3581-8c89-4c4f-86e8-6aa18bd04989" />

---

### 3.2 Verificació de fitxers HLS generats

Es comprova que el servidor genera correctament:

- Fitxers `.m3u8` (playlist)
- Fitxers `.ts` (segments de vídeo)

Això confirma que el sistema HLS funciona correctament.

<img width="940" height="473" alt="image" src="https://github.com/user-attachments/assets/d7cfaaa1-da4a-4b9b-bc37-3644daf211ce" />

---

## 4) Monitorització del servidor

### 4.1 Estadístiques RTMP

S’accedeix al panell d’estadístiques del servidor per visualitzar:

- Stream actiu
- Nombre de clients
- Bitrate
- Estat de la connexió

<img width="940" height="373" alt="image" src="https://github.com/user-attachments/assets/9ca66911-0174-471d-9778-4d0fc3acf371" />

---

### 4.2 Logs del contenidor

Es revisen els logs per verificar:

- Connexions RTMP entrants
- Execució del transcoding
- Generació de segments HLS

<img width="940" height="465" alt="image" src="https://github.com/user-attachments/assets/69a0aa21-7eff-4d1c-b317-c7083794b41c" />


---

## 5) Proves i validació final

### 5.1 Reproducció amb VLC

Es prova la reproducció del stream mitjançant VLC utilitzant la URL HLS.

<img width="940" height="373" alt="image" src="https://github.com/user-attachments/assets/bf2317d9-d355-4e05-b6af-1efd0187654b" />

---

## 6) Qüestions

### Qüestió 1: Formats i Protocols

| Característica | RTMP | HLS | DASH |
|---------------|------|------|------|
| Protocol transport | TCP | HTTP | HTTP |
| Latència típica | 2–5 s | 6–30 s | 4–20 s |
| Suport navegadors | No natiu | Sí (Safari natiu) | Via reproductor JS |
| Format segments | FLV continu | .ts + .m3u8 | .m4s + .mpd |
| Streaming adaptatiu | No | Sí | Sí |

---

### Qüestió 2: Càlculs de Bitrate

a) 5 Mbps × 100 usuaris = **500 Mbps**

b)  
50 × 5 Mbps = 250 Mbps  
30 × 2,5 Mbps = 75 Mbps  
20 × 1 Mbps = 20 Mbps  
Total = **345 Mbps**

c)  
5 Mbps ≈ 0,625 MB/s  
En 1 hora: 0,625 × 3600 = 2250 MB  
Tamany aproximat: **2,2 – 2,3 GB**

---

### Qüestió 3: Transcoding

**a) Què és el transcoding?**  
És el procés de convertir un flux de vídeo a diferents qualitats o formats per adaptar-lo a diferents dispositius i connexions.

**b) On-the-fly vs pregravat**

On-the-fly:
- Es fa en temps real
- Requereix més CPU
- S’utilitza en directes

Pregravat:
- Es genera abans de publicar
- No consumeix CPU durant reproducció
- Ideal per plataformes VOD

**c) Preset veryfast**

El preset `veryfast` és un equilibri entre:
- Baix ús de CPU
- Bona qualitat
- Baixa latència

Altres presets prioritzen qualitat però augmenten consum de recursos.

---

## 7) Reflexió final

Durant aquesta pràctica he après com funciona un sistema complet de streaming en directe utilitzant RTMP i HLS. La part més complexa ha estat entendre la configuració del transcoding i assegurar que totes les qualitats es generaven correctament.

He pogut observar les diferències entre RTMP (baixa latència però no compatible directament amb navegadors) i HLS (major latència però compatible amb web i adaptatiu).

El streaming adaptatiu millora l’experiència de l’usuari, però augmenta considerablement el consum de CPU i amplada de banda.

En un entorn real, aquest sistema podria utilitzar-se per classes online, esdeveniments en directe o retransmissions corporatives.

