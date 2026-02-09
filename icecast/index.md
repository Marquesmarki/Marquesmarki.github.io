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

<img width="933" height="480" alt="image" src="https://github.com/user-attachments/assets/08f2b251-a0b2-4bdb-8cbc-04ce8008e9f4" />

---

### Incorporació de fitxers d’àudio

S’afegeixen fitxers MP3 que s’utilitzaran com a font d’àudio per a l’streaming.

<img width="940" height="183" alt="image" src="https://github.com/user-attachments/assets/567e0687-ddd0-427e-9647-59ff92f70bda" />
<img width="940" height="190" alt="image" src="https://github.com/user-attachments/assets/521d9d32-b282-4679-8653-e848e86af5c7" />


---

## 3) Configuració d’Icecast

### Fitxer `config/icecast.xml`

Es configura el fitxer principal d’Icecast amb:
- Personalització del servidor (nom, host, administrador)
- Límits de connexió
- Ports del servei
- Paràmetres de seguretat

<img width="1124" height="883" alt="Captura de pantalla 2026-02-06 152646" src="https://github.com/user-attachments/assets/45f1ca6b-c734-46da-9a02-71683a073c6a" />

---

### Autenticació i contrasenyes

Es defineixen les contrasenyes per:
- Source
- Relay
- Administració

<img width="898" height="774" alt="image" src="https://github.com/user-attachments/assets/6058cf00-c0b9-4d1a-bc46-4ba1e656992a" />

---

### Mount point principal i metadades

Es configura el **mount point principal** amb les metadades del stream (nom, descripció i gènere).

<img width="902" height="778" alt="image" src="https://github.com/user-attachments/assets/1ac2aa07-7cba-4370-a8cd-f589b5038069" />

---

## 4) Desplegament amb Docker Compose

### Fitxer `docker-compose.yml`

Es defineixen els serveis següents:
- Servei Icecast
- Servei streamer amb FFmpeg
- Volums i xarxes
- Variables d’entorn i reinici automàtic

<img width="1200" height="948" alt="Captura de pantalla 2026-02-06 153550" src="https://github.com/user-attachments/assets/bd5a3efd-1c2c-4a77-9114-e9066d10e002" />

---

### Posada en marxa dels contenidors

S’aixequen els contenidors amb Docker Compose.

<img width="940" height="258" alt="image" src="https://github.com/user-attachments/assets/facab1f1-2ede-4aff-b41a-fc1133d01ece" />
<img width="940" height="67" alt="image" src="https://github.com/user-attachments/assets/a97ff6a5-f632-48c8-b23a-7d28fdeccb50" />

---

### Verificació d’estat i logs

Es comprova que els contenidors estan en execució i que no hi ha errors als logs.

<img width="940" height="65" alt="image" src="https://github.com/user-attachments/assets/11040e56-6822-4a61-9ff9-a6d32861151b" />
<img width="940" height="294" alt="image" src="https://github.com/user-attachments/assets/9f29b889-f0f6-4e10-840f-a5d499a62764" />
<img width="940" height="492" alt="image" src="https://github.com/user-attachments/assets/23afdc12-055d-417d-8ef7-ada3661ba4c7" />

---

## 5) Verificació del servei

### Accés a la interfície web d’Icecast

S’accedeix a la pàgina principal d’Icecast des del navegador.

<img width="940" height="454" alt="image" src="https://github.com/user-attachments/assets/813af2ba-80e4-4f70-a1e8-f608601f1163" />

---

### Reproducció del stream

Es comprova la reproducció del stream mitjançant navegador web i VLC.

<img width="940" height="458" alt="image" src="https://github.com/user-attachments/assets/947ee67e-c263-466a-9223-d6fbfa4e48d2" />

---

## 6) Configuració avançada

### Segon mount point MP3 d’alta qualitat (HQ)

Es crea un segon mount point amb major qualitat d’àudio.

<img width="940" height="938" alt="image" src="https://github.com/user-attachments/assets/ae1d6b6b-bb2a-4135-b8d3-e7fe88bff7fb" />

---

### Segon streamer per al stream HQ

Es configura un segon procés FFmpeg per al stream d’alta qualitat.

<img width="940" height="940" alt="image" src="https://github.com/user-attachments/assets/2f0463cf-bfc3-4cdb-9943-83046e3e6426" />

---

### Reinici i comprovació dels mount points

Es reinicia el servei i es comprova que tots els mount points funcionen correctament.

<img width="940" height="994" alt="image" src="https://github.com/user-attachments/assets/4b45dbbc-e18b-449b-9bb8-5c28cec90bd9" />

---

## 7) Accés a l’administració

### Panell d’administració

S’accedeix al panell d’administració d’Icecast per gestionar fonts i connexions.

<img width="940" height="473" alt="image" src="https://github.com/user-attachments/assets/d2b26d08-8160-4bf5-b7e0-818bff6e1f14" />

---

### Estadístiques i gestió de fonts

Es visualitzen les estadístiques de connexió i les fonts actives.

<img width="940" height="356" alt="image" src="https://github.com/user-attachments/assets/272cae14-c2ca-44be-9eba-add9d7c16eb1" />
<img width="940" height="358" alt="image" src="https://github.com/user-attachments/assets/62647eb5-a0f3-461f-85f2-f07fc650c1f9" />

---

## 8) Streaming en format Opus (opcional)

### Mount point en format Opus

Es crea un mount point addicional utilitzant el format Opus.

<img width="940" height="1019" alt="image" src="https://github.com/user-attachments/assets/fbdacdc7-29fe-482a-a19f-90196fe74af1" />

---

### Streamer Opus amb FFmpeg

Es configura FFmpeg per emetre en format Opus.

<img width="940" height="944" alt="image" src="https://github.com/user-attachments/assets/527f19bd-0e32-4472-8b5a-0196c669bd79" />

---

### Comparativa de qualitat i compatibilitat

Es comparen els formats MP3 i Opus en termes de qualitat i compatibilitat.

<img width="873" height="441" alt="image" src="https://github.com/user-attachments/assets/6b60af95-49a0-4266-9191-1ebdc79c9699" />

---

## 9) Monitorització i estadístiques

### Estadístiques en temps real

Es visualitzen les estadístiques en temps real des de la interfície web.

<img width="940" height="471" alt="image" src="https://github.com/user-attachments/assets/bf7dc56c-e293-4945-98b6-4e9bf0b7891e" />

---

### Anàlisi de logs

Es revisen els logs d’Icecast per detectar accessos i possibles errors.

<img width="940" height="625" alt="image" src="https://github.com/user-attachments/assets/e65a19d1-40c9-483a-873a-ede6c82b9eef" />

---

## 10) Captures obligatòries

- Contenidors actius (terminal)
- 
  <img width="940" height="213" alt="image" src="https://github.com/user-attachments/assets/2ba781f0-c277-425e-bbf0-98f32c03b645" />
  
- Pàgina principal d’Icecast amb mount points

  <img width="940" height="456" alt="image" src="https://github.com/user-attachments/assets/a15dc2df-02bd-4c0b-bb5e-cf3422e259be" />

- Reproducció del stream

  <img width="940" height="465" alt="image" src="https://github.com/user-attachments/assets/83e68424-2050-4bd3-87e2-c7bfd775a5e7" />

- Panell d’administració

  <img width="940" height="473" alt="image" src="https://github.com/user-attachments/assets/9b005ecd-65eb-4bc6-a5d2-ec105488492a" />
   
- Logs amb connexió del source  

  <img width="940" height="444" alt="image" src="https://github.com/user-attachments/assets/52942e39-46b9-43f7-aec8-0f8142767cfc" />

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

<img width="940" height="790" alt="image" src="https://github.com/user-attachments/assets/2ff17aa6-3818-4af9-ab53-9b71d354f64a" />

Resultat

<img width="940" height="598" alt="image" src="https://github.com/user-attachments/assets/ad829faa-9c99-4c74-bdd9-27681d30e29c" />

---

### Metadades dinàmiques

Configuració de metadades canviants durant l’emissió.

<img width="940" height="296" alt="image" src="https://github.com/user-attachments/assets/892d32af-627f-4adb-b460-5ec8f85a11a2" />

Resultat

<img width="940" height="571" alt="image" src="https://github.com/user-attachments/assets/362db8f9-d146-4a88-bd2e-1fb2f6ded317" />

---

### Programació horària

Execució de l’streaming mitjançant scripts i cron.

<img width="940" height="252" alt="image" src="https://github.com/user-attachments/assets/6f56e867-0ac7-466f-ac5d-0c1ba793832f" />
<img width="940" height="494" alt="image" src="https://github.com/user-attachments/assets/e844dd20-7b13-4390-b190-28ef3289ad76" />


---

## 14) Reflexió personal

Durant aquesta pràctica he après com funciona una ràdio per Internet i la importància d’una bona configuració del servei. Docker facilita molt el desplegament i el manteniment del sistema, permetent reiniciar el servei fàcilment i tenir un entorn controlat.

---

## 15) Conclusions

Icecast és una solució robusta i flexible per a la creació de ràdios per Internet, ideal tant per a projectes educatius com personals, oferint múltiples formats, qualitat d’àudio configurable i una gestió senzilla del servei.
