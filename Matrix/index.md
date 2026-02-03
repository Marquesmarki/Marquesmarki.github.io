# NF3 – Servidor de Missatgeria Matrix amb Synapse i Element

**Mòdul:** M0375 – Serveis de xarxa i Internet  
**Pràctica:** NF3 – Servidor de missatgeria segura  
**Alumne:** Alex Marques  
**Tecnologia:** Matrix + Synapse + Element + Docker  

---

## Objectiu de la pràctica

L’objectiu d’aquesta pràctica és desplegar i configurar un **servidor de missatgeria instantània Matrix** utilitzant **Synapse** com a homeserver, gestionat amb **Docker Compose**, i verificar el seu funcionament mitjançant el client web **Element**, fent ús de **xifrat d’extrem a extrem (E2EE)**.

---

## Índex

1. Requisits previs  
2. Desplegament del servidor Matrix  
3. Verificació del funcionament del servidor  
4. Accés i configuració del client Element  
5. Creació i gestió d’usuaris  
6. Creació i configuració de sales  
7. Proves de missatgeria segura (E2EE)  
8. Funcionalitats avançades  
9. Administració del servidor  
10. Client de terminal (opcional)  
11. Qüestions finals  

---

## 1) Requisits previs

- Docker
- Connexió a Internet
- Navegador web
- Coneixements bàsics de contenidors
- Port 8008 accessible

---

## 2) Desplegament del servidor Matrix

### Inici dels contenidors amb Docker Compose

S’ha desplegat el servidor Matrix mitjançant Docker Compose, creant els contenidors corresponents a **Synapse**.

<img width="940" height="717" alt="image" src="https://github.com/user-attachments/assets/b24c4489-6c43-4695-9381-f1318fbca91f" />

---

## 3) Verificació del funcionament del servidor

Un cop aixecat el servei, s’han revisat els **logs del contenidor Synapse** per comprovar que el servidor s’inicia correctament i queda a l’espera de connexions.

<img width="940" height="306" alt="image" src="https://github.com/user-attachments/assets/e1d652c5-58ad-400a-b6e7-e0cb9a3ac9d8" />

---

## 4) Accés al client Element

S’accedeix al client web **Element**, que actua com a interfície gràfica del servidor Matrix.

<img width="940" height="473" alt="image" src="https://github.com/user-attachments/assets/e4875e5e-4f3f-498e-83bf-0afe23e3ea44" />

---

## 5) Creació i gestió d’usuaris

### Creació de l’usuari administrador

Es crea un primer usuari amb rol d’administrador per gestionar el servidor.

<img width="940" height="467" alt="image" src="https://github.com/user-attachments/assets/b9f61466-84ba-4179-8a25-d45aa9e6a7a1" />

---

### Registre d’usuaris addicionals

Es registren diversos usuaris addicionals per realitzar les proves de missatgeria.

<img width="940" height="450" alt="image" src="https://github.com/user-attachments/assets/7a5bc5e3-0a4b-49b4-83db-c9e30f1116c9" />
<img width="940" height="469" alt="image" src="https://github.com/user-attachments/assets/142a8fad-79b3-47d1-be75-0829a7fded09" />

---

## 6) Creació i configuració de sales

### Creació d’una sala de xat

Es crea una sala personalitzada que servirà per fer les proves de comunicació.

<img width="940" height="475" alt="image" src="https://github.com/user-attachments/assets/7368eb7d-75c4-4227-8b14-65c10f09312a" />

---

### Activació del xifrat E2EE

A la configuració de la sala s’activa el **xifrat d’extrem a extrem**, garantint la confidencialitat dels missatges.

<img width="940" height="479" alt="image" src="https://github.com/user-attachments/assets/15a38355-b538-4c31-bc31-7ecfe6ee7dcb" />

---

### Invitació d’usuaris a la sala

Els usuaris creats anteriorment són convidats a participar a la sala.

<img width="940" height="481" alt="image" src="https://github.com/user-attachments/assets/9ad3f0e4-4888-42aa-8682-5169d39891e3" />

<img width="940" height="352" alt="image" src="https://github.com/user-attachments/assets/1b6a2ccc-40b1-4737-8455-05a6330c24db" />


---

## 7) Proves de missatgeria segura

### Conversa amb xifrat E2EE actiu

Es verifica que la sala indica correctament que el xifrat d’extrem a extrem està habilitat.

<img width="940" height="498" alt="image" src="https://github.com/user-attachments/assets/5c5b9cd8-2c91-4bb3-b6ea-a84a7c9495bb" />

---

### Intercanvi de missatges

Els usuaris intercanvien missatges comprovant que la comunicació funciona correctament.

<img width="940" height="477" alt="image" src="https://github.com/user-attachments/assets/ce4c65be-bb6c-4ce7-a9cc-78c11aa1ad5d" />

---

### Verificació de dispositius

Els dispositius dels usuaris es verifiquen mútuament per garantir la confiança del xifrat.

<img width="940" height="479" alt="image" src="https://github.com/user-attachments/assets/6871b033-92ab-4168-95c1-476d3e538772" />

---

## 8) Funcionalitats avançades

### Enviament i descàrrega de fitxers

S’envien fitxers dins de la sala xifrada i es comprova que es poden descarregar correctament.

<img width="940" height="498" alt="image" src="https://github.com/user-attachments/assets/ccb06f60-c2bf-4794-8a1a-ff24526e480a" />

---

### Missatges amb format Markdown

Es comprova el suport de Markdown per donar format als missatges.

<img width="940" height="265" alt="image" src="https://github.com/user-attachments/assets/0b7f58ed-cca0-4176-bfc4-d1ecfd53dcb3" />

---

### Reaccions i respostes

Es fan servir reaccions i respostes als missatges.

<img width="940" height="358" alt="image" src="https://github.com/user-attachments/assets/ae32bf80-ac04-4811-b0dd-e8b59334ac91" />

---

## 9) Administració del servidor

### Desactivació del registre obert

Per millorar la seguretat, es desactiva el registre obert d’usuaris al servidor.

<img width="940" height="996" alt="image" src="https://github.com/user-attachments/assets/f9be3c3a-f285-4bea-ac8a-d47f3286676c" />

---

### Monitorització de recursos

Es comprova l’ús de CPU, memòria i disc dels contenidors.

<img width="940" height="208" alt="image" src="https://github.com/user-attachments/assets/fe60f65f-6682-427f-9575-00db57b97190" />

---

### Revisió de logs

Es revisen els logs d’activitat del servidor Matrix.

<img width="940" height="560" alt="image" src="https://github.com/user-attachments/assets/e807187b-b8cc-4634-b5b7-54493a0f0f28" />

---

## 10) Client de terminal (opcional)

### Connexió amb gomuks

S’utilitza el client de terminal **gomuks** per connectar-se al servidor Matrix.

<img width="940" height="690" alt="image" src="https://github.com/user-attachments/assets/edb182be-f3dd-4d96-9e34-7330e18b2f4c" />

---

## 11) Qüestions finals

### Qüestió 1: Federació a Matrix

La federació permet que diferents servidors Matrix es comuniquin entre ells.  
Cada usuari pertany a un **homeserver**, però pot parlar amb usuaris d’altres servidors.

És important perquè:
- No depèn d’una sola empresa
- És descentralitzat
- Evita punts únics de fallada

---

### Qüestió 2: Diferència entre Matrix i WhatsApp

**Matrix**
- Descentralitzat  
- Codi obert  
- Control total del servidor  

**WhatsApp**
- Centralitzat  
- Depèn de Meta  
- No és de codi obert  

---

### Qüestió 3: Què és un homeserver?

Un **homeserver** és el servidor on es registren els usuaris Matrix.  
Les seves funcions principals són:
- Gestionar comptes
- Gestionar sales
- Emmagatzemar missatges
- Controlar el xifrat

---

## 12) Exercicis opcionals

A continuació es mostren els **exercicis opcionals** realitzats sobre el servidor Matrix desplegat, seguint les indicacions de la pràctica.

---

### Exercici 1: Creació d’una sala pública

Es crea una **sala pública** dins del servidor Matrix per permetre l’accés a qualsevol usuari del servidor.

Accions realitzades:
- Creació d’una nova sala des del client Element
- Assignació de nom i descripció
- Configuració de la sala com a **pública**
- Verificació que apareix al directori de sales

La sala queda accessible per a altres usuaris i permet comprovar el funcionament de les sales obertes a Matrix.

<img width="940" height="496" alt="image" src="https://github.com/user-attachments/assets/324ffd52-2b91-4db3-abc2-3350214d31b3" />

---

### Exercici 2: Bot simple (avançat)

Es crea un **bot simple** que es connecta al servidor Matrix des del terminal i interactua dins d’una sala.

Funcionalitats comprovades:
- Connexió del bot al servidor Matrix des del terminal
- Invitació del bot a una sala
- Enviament automàtic de missatges
- Resposta del bot a paraules clau (exemple: `hola`)

El bot demostra la possibilitat d’integrar **clients automatitzats** al servidor Matrix.

<img width="940" height="83" alt="image" src="https://github.com/user-attachments/assets/8b36bef9-134b-4743-bb5b-79075574792d" />

<img width="931" height="213" alt="image" src="https://github.com/user-attachments/assets/937070c1-e882-4f95-9409-a738b34b107f" />

<img width="941" height="192" alt="image" src="https://github.com/user-attachments/assets/ca2f3530-e80d-4c7d-b1d4-7ec3ce314ea1" />

---

### Exercici 3: Backup de dades del servidor

Es realitza una **còpia de seguretat completa** del servidor Matrix mitjançant un script.

Procés realitzat:
- Aturada del contenidor Synapse
- Compressió de les dades del servidor
- Creació d’un fitxer `.tar.gz` amb data
- Verificació de la còpia generada

Elements inclosos al backup:
- Directori de dades de Synapse
- Base de dades
- Configuració del servidor

Aquest procediment permet garantir la **recuperació del servei** en cas de fallada o migració.

<img width="940" height="230" alt="image" src="https://github.com/user-attachments/assets/0fbf36d3-3b70-4402-b5aa-6b1d3aa926dd" />

<img width="941" height="99" alt="image" src="https://github.com/user-attachments/assets/d181a81f-5aac-4dd9-9aa4-c87b00dc3fae" />

---


## Reflexió personal

Durant aquesta pràctica he après com funciona la missatgeria descentralitzada i quins avantatges té Matrix davant d’altres aplicacions més conegudes. Al principi, la configuració del servidor Synapse amb Docker ha estat la part més complicada, sobretot pel tema dels ports, la xarxa i la creació d’usuaris, però això m’ha ajudat a entendre millor com funcionen els contenidors i els serveis en xarxa.

També he pogut comprendre la importància del xifrat d’extrem a extrem (E2EE) i la verificació de dispositius per garantir la seguretat de les comunicacions. A diferència de plataformes com WhatsApp o Telegram, Matrix permet tenir més control sobre les dades, ja que es pot auto-allotjar el servidor.

L’auto-allotjament ofereix avantatges com la independència de serveis externs i un major control de la informació, tot i que també requereix més responsabilitat en el manteniment i la seguretat del sistema.

En un entorn real, considero que Matrix seria útil en centres educatius, empreses o equips de treball que necessitin comunicacions privades i segures. Aquesta pràctica m’ha ajudat a entendre millor com funcionen les plataformes de missatgeria actuals i la seva utilitat en entorns professionals.
