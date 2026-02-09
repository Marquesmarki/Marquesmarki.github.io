# NF – Servidor de Streaming amb Icecast i Docker

**Mòdul:** M0375 – Serveis de xarxa i Internet  
**Pràctica:** Servidor de ràdio per Internet amb Icecast  
**Alumne:** Alex Marques  
**Tecnologies:** Icecast + FFmpeg + Docker Compose  

---

## 1) Objectius de la pràctica

### Objectius generals
- Desplegar un servidor de ràdio per Internet amb Icecast
- Emissió d’àudio en streaming mitjançant Docker
- Configurar diferents formats i qualitats d’àudio

### Resultats esperats
- Servei Icecast funcional
- Reproducció del stream des de navegador i VLC
- Gestió de múltiples mount points

---

## 2) Requisits previs

### Programari necessari
- Docker
- Docker Compose
- Navegador web o VLC

### Coneixements previs
- Contenidors Docker
- Fitxers de configuració XML i YAML
- Conceptes bàsics de streaming

### Fitxers d’àudio
- Fitxers MP3 utilitzats amb llicència lliure o pròpia

---

## 3) Preparació de l’entorn

### 3.1 Estructura de directoris

icecast-AlexMarques/
├── audio/
├── config/
│ └── icecast.xml
├── docker-compose.yml


### 3.2 Incorporació de fitxers d’àudio

Els fitxers MP3 es col·loquen dins del directori `audio/` per ser utilitzats pel streamer.

---

## 4) Configuració d’Icecast

### 4.1 Fitxer `config/icecast.xml`

Configuració principal:
- Nom del servidor
- Host i administrador
- Contrasenyes (source, relay, admin)
- Límit de connexions
- Mount point principal

### 4.2 Fitxer `docker-compose.yml`

Serveis configurats:
- **Icecast** (servidor)
- **Streamer (FFmpeg)**

Configuració de:
- Ports
- Volums
- Xarxa
- Variables d’entorn
- Reinici automàtic

---

## 5) Desplegament amb Docker Compose

### 5.1 Posada en marxa

S’aixequen els contenidors amb Docker Compose.

### 5.2 Verificació d’estat

Es comprova que els contenidors estan actius.

### 5.3 Revisió de logs

Es revisen els logs per assegurar que Icecast i el streamer funcionen correctament.

---

## 6) Verificació del servei

### 6.1 Accés a la interfície web

S’accedeix a la pàgina principal d’Icecast des del navegador.

### 6.2 Reproducció del stream

El stream es reprodueix correctament:
- Via navegador
- Via VLC

---

## 7) Configuració avançada

### 7.1 Segon mount point MP3 (HQ)

Es crea un segon mount point amb qualitat alta:
- MP3 320 kbps

### 7.2 Segon streamer

Es configura un segon streamer FFmpeg per al stream HQ.

### 7.3 Comprovació

Es verifiquen tots els mount points disponibles.

---

## 8) Accés a l’administració

### 8.1 Panell d’administració

Accés mitjançant credencials d’administrador.

### 8.2 Estadístiques

Visualització de:
- Oients connectats
- Fonts actives
- Amplada de banda

---

## 9) Streaming en format Opus (opcional)

### 9.1 Mount point Opus

Creació d’un mount point amb format Opus.

### 9.2 Streamer Opus

Configuració de FFmpeg per emetre en Opus.

### 9.3 Comparativa

- Opus: millor compressió
- MP3: més compatibilitat

---

## 10) Monitorització i estadístiques

### 10.1 Estadístiques en temps real

Consultables des de la web d’Icecast.

### 10.2 Anàlisi de logs

Revisió d’accessos i errors del servei.

---

## 11) Captures obligatòries

- Contenidors actius (terminal)
- Pàgina principal d’Icecast
- Reproducció del stream
- Panell d’administració
- Logs amb connexió del source

---

## 12) Proves de funcionalitat

### Mount points configurats

| Mount Point | Format | Bitrate | Estat | URL |
|-----------|--------|---------|-------|-----|
| /radio-AlexMarques.mp3 | MP3 | 128 kbps | Actiu | http://localhost:8000/radio-AlexMarques.mp3 |
| /radio-AlexMarques-hq.mp3 | MP3 | 320 kbps | Actiu | http://localhost:8000/radio-AlexMarques-hq.mp3 |
| /radio-AlexMarques.opus | Opus | 96 kbps | Actiu | http://localhost:8000/radio-AlexMarques.opus |

---

## 13) Qüestions

### 13.1 Càlcul d’amplada de banda

- 15 oients a 128 kbps → **1,92 Mbps**
- Amb 10 Mbps → **78 oients aproximadament**
- Consum mensual amb 10 oients → **414,72 GB/mes**

### 13.2 Resolució d’incidències

- Contrasenya incorrecta del source
- Mount point mal configurat
- Servei Icecast aturat

---

## 14) Exercicis opcionals

### 14.1 Playlist rotativa
- Configuració d’una llista d’àudio rotativa amb FFmpeg

### 14.2 Metadades dinàmiques
- Actualització automàtica del títol de la cançó

### 14.3 Programació horària
- Execució programada mitjançant scripts i cron

---

## 15) Reflexió personal

Aquesta pràctica m’ha permès entendre com funciona el streaming d’àudio per Internet i com Docker facilita enormement el desplegament del servei. Tot i algunes dificultats inicials amb la configuració, la resolució d’errors m’ha ajudat a millorar la meva capacitat de diagnosi.

Icecast és una eina molt útil per a projectes educatius, emissores escolars, podcasts o ràdio corporativa, i representa una alternativa moderna a les ràdios tradicionals.

---

## 16) Conclusions

S’ha desplegat correctament un servidor de ràdio per Internet funcional, amb múltiples formats i qualitats, complint tots els objectius de la pràctica del mòdul M0375.

