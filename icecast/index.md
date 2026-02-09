# NF3 – Ràdio per Internet amb Icecast i Docker

**Mòdul:** M0375 – Serveis de xarxa i Internet  
**Pràctica:** NF3 – Ràdio per Internet  
**Alumne:** Alex Marques  
**Tecnologia:** Icecast + FFmpeg + Docker Compose  

---

## Objectius de la pràctica

L’objectiu d’aquesta pràctica és desplegar i configurar un **servidor de ràdio per Internet amb Icecast**, utilitzant **Docker Compose**, emetre àudio en directe mitjançant **FFmpeg**, i verificar el funcionament del servei amb diferents formats i qualitats d’àudio.

---

## Índex

1. Requisits previs  
2. Preparació de l’entorn  
3. Configuració d’Icecast  
4. Desplegament amb Docker Compose  
5. Verificació del servei  
6. Configuració avançada  
7. Accés a l’administració  
8. Streaming en format Opus (opcional)  
9. Monitorització i estadístiques  
10. Captures obligatòries  
11. Proves de funcionalitat  
12. Qüestions  
13. Exercicis opcionals  
14. Reflexió personal  
15. Conclusions  

---

## 1) Requisits previs

- Docker i Docker Compose
- Connexió a Internet
- Navegador web
- Reproductor multimèdia (VLC)
- Fitxers d’àudio en format MP3 amb llicència lliure

---

## 2) Preparació de l’entorn

### Estructura de directoris del projecte

Es crea una estructura de directoris per organitzar la configuració, els fitxers d’àudio i els scripts del projecte.

<captura aquí>

---

### Incorporació de fitxers d’àudio

S’afegeixen fitxers MP3 que s’utilitzaran com a font d’àudio per a l’streaming.

<captura aquí>

---

## 3) Configuració d’Icecast

### Fitxer `config/icecast.xml`

Es configura el fitxer principal d’Icecast amb:
- Personalització del servidor (nom, host, administrador)
- Límits de connexió
- Ports del servei
- Paràmetres de seguretat

<captura aquí>

---

### Autenticació i contrasenyes

Es defineixen les contrasenyes per:
- Source
- Relay
- Administració

<captura aquí>

---

### Mount point principal i metadades

Es configura el **mount point principal** amb les metadades del stream (nom, descripció i gènere).

<captura aquí>

---

## 4) Desplegament amb Docker Compose

### Fitxer `docker-compose.yml`

Es defineixen els serveis següents:
- Servei Icecast
- Servei streamer amb FFmpeg
- Volums i xarxes
- Variables d’entorn i reinici automàtic

<captura aquí>

---

### Posada en marxa dels contenidors

S’aixequen els contenidors amb Docker Compose.

<captura aquí>

---

### Verificació d’estat i logs

Es comprova que els contenidors estan en execució i que no hi ha errors als logs.

<captura aquí>

---

## 5) Verificació del servei

### Accés a la interfície web d’Icecast

S’accedeix a la pàgina principal d’Icecast des del navegador.

<captura aquí>

---

### Reproducció del stream

Es comprova la reproducció del stream mitjançant navegador web i VLC.

<captura aquí>

---

## 6) Configuració avançada

### Segon mount point MP3 d’alta qualitat (HQ)

Es crea un segon mount point amb major qualitat d’àudio.

<captura aquí>

---

### Segon streamer per al stream HQ

Es configura un segon procés FFmpeg per al stream d’alta qualitat.

<captura aquí>

---

### Reinici i comprovació dels mount points

Es reinicia el servei i es comprova que tots els mount points funcionen correctament.

<captura aquí>

---

## 7) Accés a l’administració

### Panell d’administració

S’accedeix al panell d’administració d’Icecast per gestionar fonts i connexions.

<captura aquí>

---

### Estadístiques i gestió de fonts

Es visualitzen les estadístiques de connexió i les fonts actives.

<captura aquí>

---

## 8) Streaming en format Opus (opcional)

### Mount point en format Opus

Es crea un mount point addicional utilitzant el format Opus.

<captura aquí>

---

### Streamer Opus amb FFmpeg

Es configura FFmpeg per emetre en format Opus.

<captura aquí>

---

### Comparativa de qualitat i compatibilitat

Es comparen els formats MP3 i Opus en termes de qualitat i compatibilitat.

---

## 9) Monitorització i estadístiques

### Estadístiques en temps real

Es visualitzen les estadístiques en temps real des de la interfície web.

<captura aquí>

---

### Anàlisi de logs

Es revisen els logs d’Icecast per detectar accessos i possibles errors.

<captura aquí>

---

## 10) Captures obligatòries

- Contenidors actius (terminal)  
- Pàgina principal d’Icecast amb mount points  
- Reproducció del stream  
- Panell d’administració  
- Logs amb connexió del source  

<captura aquí>

---

## 11) Proves de funcionalitat

| Mount point | Format | Bitrate | Estat | URL |
|------------|--------|---------|-------|-----|
| /radio-AlexMarques.mp3 | MP3 | 128 kbps | Actiu | http://localhost:8000/radio-AlexMarques.mp3 |
| /radio-AlexMarques-hq.mp3 | MP3 | 320 kbps | Actiu | http://localhost:8000/radio-AlexMarques-hq.mp3 |
| /radio-AlexMarques.opus | Opus | 96 kbps | Actiu | http://localhost:8000/radio-AlexMarques.opus |

---

## 12) Qüestions

### Càlcul d’amplada de banda

- Amb 15 oients a 128 kbps: **1,92 Mbps**
- Amb 10 Mbps de pujada: **78 oients aproximadament**
- Consum mensual amb 10 oients constants: **414,72 GB/mes**

---

### Resolució d’incidències

- Contrasenya del source incorrecta
- Mount point mal escrit
- Servei Icecast aturat o amb errors

---

## 13) Exercicis opcionals

### Playlist rotativa

Configuració d’una llista de reproducció automàtica amb FFmpeg.

<captura aquí>

---

### Metadades dinàmiques

Configuració de metadades canviants durant l’emissió.

<captura aquí>

---

### Programació horària

Execució de l’streaming mitjançant scripts i cron.

<captura aquí>

---

## 14) Reflexió personal

Durant aquesta pràctica he après com funciona una ràdio per Internet i la importància d’una bona configuració del servei. Docker facilita molt el desplegament i el manteniment del sistema, permetent reiniciar el servei fàcilment i tenir un entorn controlat.

---

## 15) Conclusions

Icecast és una solució robusta i flexible per a la creació de ràdios per Internet, ideal tant per a projectes educatius com personals, oferint múltiples formats, qualitat d’àudio configurable i una gestió senzilla del servei.
