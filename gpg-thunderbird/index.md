# NF3.1 CP1 – Pràctica OpenPGP (GPG) + Thunderbird (M0375)

**Mòdul:** M0375 Serveis de xarxa i Internet  
**Pràctica:** NF3.1_CP1_Cas Pràctic 1  
**Alumne:** Alex Marques  
**Objectiu:** Generar claus GPG, configurar Thunderbird amb OpenPGP, enviar correus **signats** i **xifrats (E2EE)**, i respondre les qüestions finals.

---

## Índex
1. Objectius i requisits  
2. Part 1 – Generació de claus GPG  
3. Part 2 – Exportació i intercanvi de claus públiques  
4. Part 3 – Configuració de Thunderbird amb GPG  
5. Part 4 – Enviament de correus signats digitalment  
6. Part 5 – Enviament de correus xifrats (E2EE)  
7. Part 6 – Proves avançades  
8. Qüestions finals  

---

## 1) Objectius i requisits

### Objectius
- Generar claus GPG/PGP per **signatura** i **xifrat**
- Configurar Thunderbird per utilitzar **OpenPGP**
- Enviar correus **signats**
- Enviar correus **xifrats d’extrem a extrem (E2EE)**
- Intercanviar **claus públiques** entre usuaris
- Verificar signatures digitals
- Entendre la diferència entre **TLS (transport)** i **GPG (end-to-end)** 

### Requisits previs
- Servidor de correu funcional (Mailcow completat)
- Mozilla Thunderbird instal·lat
- 2 comptes de correu configurats
- Coneixements bàsics de criptografia asimètrica 

---

## 2) Part 1 – Generació de claus GPG

### 2.1 Instal·lació de GPG
- Windows: instal·lació de Gpg4win
- Linux: instal·lació de `gnupg`
- Verificació: executar `gpg --version`
  <img width="940" height="321" alt="image" src="https://github.com/user-attachments/assets/a1705e0a-2161-4a46-8194-e5351c7218c5" />


### 2.2 Generació de la primera parella de claus
Comanda utilitzada:
gpg --full-generate-key

yaml
Copiar código

Configuració típica:
- Tipus: RSA i RSA
- Mida: 4096 bits
- Caducitat: 1 any
- Nom i correu: usuari 1 (ex: alex1@...)
- Contrasenya: definida a la pràctica
  <img width="940" height="525" alt="image" src="https://github.com/user-attachments/assets/419c212e-e0ee-4841-a89f-df01037c69bb" />
  <img width="940" height="488" alt="image" src="https://github.com/user-attachments/assets/f90aa777-8494-424c-b6b0-bd25263b5d10" />



### 2.3 Verificació de la clau creada
gpg --list-keys

yaml
Copiar código
S’hi comprova que apareix la clau `pub` i la subclau `sub` (xifrat).

### 2.4 Generació de la segona parella de claus
Es repeteix el mateix procés per al segon usuari (ex: alex2@...). 

**Captures (obligatòries):**
- Instal·lació / verificació `gpg --version`
- Generació de clau 1
  <img width="940" height="271" alt="image" src="https://github.com/user-attachments/assets/8ce7be13-9f02-4ad7-a9b9-cad63a77c645" />
- `gpg --list-keys`
- Generació de clau 2
  <img width="940" height="392" alt="image" src="https://github.com/user-attachments/assets/823873b0-2152-4f56-8e64-deed615953c2" />


---

## 3) Part 2 – Exportació i intercanvi de claus públiques

### 3.1 Exportar la clau pública
Exemple:
gpg --armor --export alex1@... > clau-publica-alex1.asc
gpg --armor --export alex2@... > clau-publica-alex2.asc
<img width="940" height="19" alt="image" src="https://github.com/user-attachments/assets/08dd5c55-751a-407c-8754-b4d61331be0b" />


### 3.2 Visualitzar la clau pública
type clau-publica-alex1.asc
<img width="940" height="419" alt="image" src="https://github.com/user-attachments/assets/038e5a87-363c-4c6d-b0a8-f066284c2cba" />


### 3.3 Intercanvi de claus (simulat)
Cada usuari importa la clau pública de l’altre:
gpg --import clau-publica-alex2.asc
gpg --import clau-publica-alex1.asc

<img width="940" height="165" alt="image" src="https://github.com/user-attachments/assets/4834fd74-ffc5-43af-8b9d-17670059dc99" />


### 3.4 Establir confiança (trust)
Entrar a l’editor i marcar confiança:
gpg --edit-key alex2@...
trust
5
quit

Això evita avisos i permet validar signatures amb més confiança.
<img width="940" height="263" alt="image" src="https://github.com/user-attachments/assets/2b06bda2-7c36-4f59-b529-d6b8e99e7e90" />
<img width="940" height="531" alt="image" src="https://github.com/user-attachments/assets/25b5a31a-cd62-4a5f-a87d-6c734c8d2213" />
<img width="940" height="227" alt="image" src="https://github.com/user-attachments/assets/3ecf913d-e23c-4d27-911a-7e80f7761aa5" />

---

## 4) Part 3 – Configuració de Thunderbird amb GPG (OpenPGP)

### 4.1 Habilitar OpenPGP a Thunderbird
En versions modernes, OpenPGP acostuma a venir **activat per defecte**. 
<img width="940" height="192" alt="image" src="https://github.com/user-attachments/assets/65916f22-f26e-4d7b-9d7a-c4bb877d481a" />

### 4.2 Importar la clau privada al Thunderbird (clau personal)
Per cada compte:
- Conseguir claus privades
  <img width="940" height="31" alt="image" src="https://github.com/user-attachments/assets/b5eeb193-1543-4afa-9fd8-12d3a9e3c537" />
- Thunderbird → **Eines** → **Gestor de claus OpenPGP**
  <img width="940" height="663" alt="image" src="https://github.com/user-attachments/assets/bcd020ec-76f4-415b-9e0e-34b5b5ff4f98" />
- **Importar clau OpenPGP personal existent** 
  <img width="940" height="660" alt="image" src="https://github.com/user-attachments/assets/5762d38c-d615-41dd-9d8d-11816e1bd66b" />


### 4.3 Assignar la clau al compte de correu
- Configuració del compte → **Xifrat d’extrem a extrem**
- OpenPGP → Afegir/assignar clau
- Seleccionar la clau corresponent al correu del compte 
<img width="940" height="542" alt="image" src="https://github.com/user-attachments/assets/9afe23f2-5745-4388-8109-84ecc8275bb2" />
<img width="940" height="496" alt="image" src="https://github.com/user-attachments/assets/be4c87ee-8501-4066-b0c3-f93d3faa43e1" />

---

## 5) Part 4 – Enviament de correus signats digitalment

### 5.1 Redactar un correu signat
- Redactar correu d’usuari 1 → usuari 2
- Activar **Seguretat → Firmar digitalment**
- Enviar i introduir la contrasenya de la clau quan la demani 
<img width="940" height="402" alt="image" src="https://github.com/user-attachments/assets/0e01a7f7-886c-4577-8db0-22412df954a8" />


### 5.2 Verificar la signatura al destinatari
En obrir el correu rebut, Thunderbird mostra:
- “**Firma digital correcta**” (o equivalent)
- Detalls de la clau del signant
<img width="940" height="246" alt="image" src="https://github.com/user-attachments/assets/6be7a33c-38ea-4ef3-8202-55a42d280f0c" />

---

## 6) Part 5 – Enviament de correus xifrats (E2EE)

### 6.1 Redactar un correu xifrat
- Redactar correu
- Activar **Seguretat → Xifrar**
<img width="940" height="344" alt="image" src="https://github.com/user-attachments/assets/a0382bff-3791-4687-8002-51da0ff8405d" />


### 6.2 Llegir el correu xifrat
El destinatari obre el correu i Thunderbird:
- Detecta que està xifrat
- Desxifra amb la clau privada
<img width="940" height="352" alt="image" src="https://github.com/user-attachments/assets/bbc78876-1a0c-473f-8325-7cd479c3c18d" />



### 6.3 Comprovar el xifrat sense clau privada
Per demostrar que el contingut no és llegible sense clau:
<img width="940" height="906" alt="image" src="https://github.com/user-attachments/assets/5f908443-03ff-4815-a237-134d7c3bca1c" />


---

## 7) Part 6 – Proves avançades

### 7.1 Correu signat + xifrat simultàniament
Enviar un correu amb:
- **Xifrar**
- **Firmar digitalment**

<img width="940" height="344" alt="image" src="https://github.com/user-attachments/assets/8517b719-f26a-45a7-9bc4-e588c63716f9" />

### 7.2 Revocar una clau GPG
Crear certificat de revocació:
gpg --gen-revoke alex1@... > revoke-alex1.asc

<img width="940" height="300" alt="image" src="https://github.com/user-attachments/assets/59392bca-cae6-44dc-84ad-ce3d311c2636" />


### 7.3 Publicar la clau en un servidor de claus
1) Obtenir ID de la clau:
gpg --list-keys

2) Enviar la clau:
gpg --send-keys --keyserver keys.openpgp.org <ID-CLAU>

<img width="940" height="260" alt="image" src="https://github.com/user-attachments/assets/c7df1673-ea97-491e-9de8-7e0c0b735439" />



### 7.4 Còpia de seguretat de la clau privada
Exportar clau privada:
gpg --armor --export-secret-keys alex1@... > backup-clau-privada-alex1.asc

<img width="940" height="58" alt="image" src="https://github.com/user-attachments/assets/86e430b5-fe8a-47d6-ae88-ef5fde456d68" />

---

## 8) Qüestions finals

### Qüestió 1: Criptografia asimètrica
a) **Xifrar:** s’utilitza la **clau pública del destinatari** (la pot tenir tothom, perquè es comparteix).  
b) **Desxifrar:** s’utilitza la **clau privada del destinatari** (només la té el destinatari).  
c) **Signar:** s’utilitza la **clau privada del remitent**.  
d) **Verificar signatura:** s’utilitza la **clau pública del remitent**. 

### Qüestió 2: Signatura vs Xifrat (taula)
| Característica              | Signatura Digital | Xifrat (E2EE) | Signatura + Xifrat |
|-----------------------------|------------------|--------------|-------------------|
| Garanteix confidencialitat  | No               | Sí           | Sí                |
| Garanteix autenticació      | Sí               | No           | Sí                |
| Garanteix integritat        | Sí               | No           | Sí                |
| Pot ser llegit pel servidor | Sí               | No           | No                |


### Qüestió 3: TLS vs GPG
a) **SMTP amb STARTTLS:** xifrat **en trànsit** (entre servidors). Els servidors poden llegir el correu quan el desencripten per emmagatzemar-lo.  
b) **GPG/PGP (E2EE):** xifrat **d’extrem a extrem**. Només el destinatari amb la seva clau privada pot llegir el contingut.  
c) **Per què usar tots dos:** TLS protegeix el transport; GPG protegeix el contingut fins i tot si el servidor o el trànsit es veuen compromesos. :contentReference[oaicite:31]{index=31}

### Qüestió 4: Escenaris d’ús
a) Metge → informe mèdic confidencial: **Xifrat + Signatura**  
b) Empresa → factura (no confidencial, però autèntica): **Signatura**  
c) Periodista ← informació sensible d’una font: **Xifrat**  
d) Advocat → contracte legal: **Xifrat + Signatura**

[Tornar a la pàgina principal](../)
