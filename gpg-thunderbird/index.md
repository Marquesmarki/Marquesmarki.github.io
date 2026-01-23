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


---

## 4) Part 3 – Configuració de Thunderbird amb GPG (OpenPGP)

### 4.1 Habilitar OpenPGP a Thunderbird
En versions modernes, OpenPGP acostuma a venir **activat per defecte**. 

### 4.2 Importar la clau privada al Thunderbird (clau personal)
Per cada compte:
- Thunderbird → **Eines** → **Gestor de claus OpenPGP**
- **Importar clau OpenPGP personal existent** (fitxer `.asc` privat)

Opcional: generar el fitxer de clau privada amb:
gpg --armor --export-secret-key alex1@... > clau-privada-alex1.asc

markdown
Copiar código


### 4.3 Assignar la clau al compte de correu
- Configuració del compte → **Xifrat d’extrem a extrem**
- OpenPGP → Afegir/assignar clau
- Seleccionar la clau corresponent al correu del compte 

**Captures (obligatòries):**
- Gestor de claus OpenPGP amb les claus importades
- Pantalla d’assignació de clau al compte 

---

## 5) Part 4 – Enviament de correus signats digitalment

### 5.1 Redactar un correu signat
- Redactar correu d’usuari 1 → usuari 2
- Activar **Seguretat → Firmar digitalment**
- Enviar i introduir la contrasenya de la clau quan la demani 

### 5.2 Verificar la signatura al destinatari
En obrir el correu rebut, Thunderbird mostra:
- “**Firma digital correcta**” (o equivalent)
- Detalls de la clau del signant 

**Captures (obligatòries):**
- Menú de redacció amb “Firmar digitalment”
- Correu rebut amb “signatura correcta” 

---

## 6) Part 5 – Enviament de correus xifrats (E2EE)

### 6.1 Redactar un correu xifrat
- Redactar correu
- Activar **Seguretat → Xifrar**
- (Recomanat) activar també **Firmar digitalment** per combinar autenticació + confidencialitat 

### 6.2 Llegir el correu xifrat
El destinatari obre el correu i Thunderbird:
- Detecta que està xifrat
- Desxifra amb la clau privada (pot demanar contrasenya)
- Mostra que el missatge està **xifrat** i (si toca) **signat** 

### 6.3 Comprovar el xifrat sense clau privada
Per demostrar que el contingut no és llegible sense clau:
- Visualitzar el “codi font” / contingut brut del missatge i comprovar que el contingut no apareix en clar (format OpenPGP/MIME).

**Captures (obligatòries):**
- Menú de redacció amb “Xifrar”
- Correu rebut mostrant que està xifrat
- Vista del contingut brut / codi font on es vegi que no està en clar

---

## 7) Part 6 – Proves avançades

### 7.1 Correu signat + xifrat simultàniament
Enviar un correu amb:
- **Xifrar**
- **Firmar digitalment**

Això aporta:
- Autenticació (signatura)
- Integritat (no modificació)
- Confidencialitat (E2EE) 

### 7.2 Revocar una clau GPG
Crear certificat de revocació:
gpg --gen-revoke alex1@... > revoke-alex1.asc

perl
Copiar código
Guardar el fitxer en lloc segur. 

### 7.3 Publicar la clau en un servidor de claus
1) Obtenir ID de la clau:
gpg --list-keys

yaml
Copiar código
2) Enviar la clau:
gpg --send-keys --keyserver keys.openpgp.org <ID-CLAU>

makefile
Copiar código
:contentReference[oaicite:26]{index=26}

### 7.4 Còpia de seguretat de la clau privada
Exportar clau privada:
gpg --armor --export-secret-keys alex1@... > backup-clau-privada-alex1.asc

yaml
Copiar código
**Important:** fitxer molt sensible; cal guardar-lo xifrat i protegit.

**Captures (obligatòries):**
- Enviament signat + xifrat
- Revocació (comanda + fitxer creat)
- Publicació (ID de clau + intent d’enviament)
- Backup de clau privada (comanda + fitxer)

---

## 8) Qüestions finals

### Qüestió 1: Criptografia asimètrica
a) **Xifrar:** s’utilitza la **clau pública del destinatari** (la pot tenir tothom, perquè es comparteix).  
b) **Desxifrar:** s’utilitza la **clau privada del destinatari** (només la té el destinatari).  
c) **Signar:** s’utilitza la **clau privada del remitent**.  
d) **Verificar signatura:** s’utilitza la **clau pública del remitent**. 

### Qüestió 2: Signatura vs Xifrat (taula)
| Característica | Signatura Digital | Xifrat (E2EE) | Signatura + Xifrat |
|---|---|---|---|
| Garanteix confidencialitat | No | Sí | Sí |
| Garanteix autenticació | Sí | No | Sí |
| Garanteix integritat | Sí | No | Sí |
| Pot ser llegit pel servidor | Sí | No | No |
| Requereix clau pública del destinatari | No | Sí | Sí | 

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
