# NF3.1 CP1 – Pràctica OpenPGP (GPG) + Thunderbird (M0375)

**Mòdul:** M0375 Serveis de xarxa i Internet  
**Pràctica:** NF3.1_CP1_Cas Pràctic 1  
**Alumne:** Alex Marques  
**Objectiu:** Generar claus GPG, configurar Thunderbird amb OpenPGP, enviar correus **signats** i **xifrats (E2EE)**, i respondre les qüestions finals. :contentReference[oaicite:0]{index=0}

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
- Entendre la diferència entre **TLS (transport)** i **GPG (end-to-end)** :contentReference[oaicite:1]{index=1}

### Requisits previs
- Servidor de correu funcional (Mailcow completat)
- Mozilla Thunderbird instal·lat
- 2 comptes de correu configurats
- Coneixements bàsics de criptografia asimètrica :contentReference[oaicite:2]{index=2}

---

## 2) Part 1 – Generació de claus GPG

### 2.1 Instal·lació de GPG
- Windows: instal·lació de Gpg4win
- Linux: instal·lació de `gnupg`
- Verificació: executar `gpg --version` :contentReference[oaicite:3]{index=3}

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
- Contrasenya: definida a la pràctica :contentReference[oaicite:4]{index=4}

### 2.3 Verificació de la clau creada
gpg --list-keys

yaml
Copiar código
S’hi comprova que apareix la clau `pub` i la subclau `sub` (xifrat). :contentReference[oaicite:5]{index=5}

### 2.4 Generació de la segona parella de claus
Es repeteix el mateix procés per al segon usuari (ex: alex2@...). :contentReference[oaicite:6]{index=6}

**Captures (obligatòries):**
- Instal·lació / verificació `gpg --version`
- Generació de clau 1
- `gpg --list-keys`
- Generació de clau 2 :contentReference[oaicite:7]{index=7}

---

## 3) Part 2 – Exportació i intercanvi de claus públiques

### 3.1 Exportar la clau pública
Exemple:
gpg --armor --export alex1@... > clau-publica-alex1.asc
gpg --armor --export alex2@... > clau-publica-alex2.asc

perl
Copiar código
`--armor` genera un fitxer ASCII fàcil de compartir. :contentReference[oaicite:8]{index=8}

### 3.2 Visualitzar la clau pública
type clau-publica-alex1.asc

perl
Copiar código
(En Linux es pot fer amb `cat`.) :contentReference[oaicite:9]{index=9}

### 3.3 Intercanvi de claus (simulat)
Cada usuari importa la clau pública de l’altre:
gpg --import clau-publica-alex2.asc
gpg --import clau-publica-alex1.asc

makefile
Copiar código
:contentReference[oaicite:10]{index=10}

### 3.4 Establir confiança (trust)
Entrar a l’editor i marcar confiança:
gpg --edit-key alex2@...
trust
5
quit

markdown
Copiar código
Això evita avisos i permet validar signatures amb més confiança. :contentReference[oaicite:11]{index=11}

**Captures (obligatòries):**
- Exportació clau pública
- Importació entre usuaris
- `gpg --edit-key` + `trust` :contentReference[oaicite:12]{index=12}

---

## 4) Part 3 – Configuració de Thunderbird amb GPG (OpenPGP)

### 4.1 Habilitar OpenPGP a Thunderbird
En versions modernes, OpenPGP acostuma a venir **activat per defecte**. :contentReference[oaicite:13]{index=13}

### 4.2 Importar la clau privada al Thunderbird (clau personal)
Per cada compte:
- Thunderbird → **Eines** → **Gestor de claus OpenPGP**
- **Importar clau OpenPGP personal existent** (fitxer `.asc` privat)

Opcional: generar el fitxer de clau privada amb:
gpg --armor --export-secret-key alex1@... > clau-privada-alex1.asc

markdown
Copiar código
:contentReference[oaicite:14]{index=14}

### 4.3 Assignar la clau al compte de correu
- Configuració del compte → **Xifrat d’extrem a extrem**
- OpenPGP → Afegir/assignar clau
- Seleccionar la clau corresponent al correu del compte :contentReference[oaicite:15]{index=15}

**Captures (obligatòries):**
- Gestor de claus OpenPGP amb les claus importades
- Pantalla d’assignació de clau al compte :contentReference[oaicite:16]{index=16}

---

## 5) Part 4 – Enviament de correus signats digitalment

### 5.1 Redactar un correu signat
- Redactar correu d’usuari 1 → usuari 2
- Activar **Seguretat → Firmar digitalment**
- Enviar i introduir la contrasenya de la clau quan la demani :contentReference[oaicite:17]{index=17}

### 5.2 Verificar la signatura al destinatari
En obrir el correu rebut, Thunderbird mostra:
- “**Firma digital correcta**” (o equivalent)
- Detalls de la clau del signant :contentReference[oaicite:18]{index=18}

**Captures (obligatòries):**
- Menú de redacció amb “Firmar digitalment”
- Correu rebut amb “signatura correcta” :contentReference[oaicite:19]{index=19}

---

## 6) Part 5 – Enviament de correus xifrats (E2EE)

### 6.1 Redactar un correu xifrat
- Redactar correu
- Activar **Seguretat → Xifrar**
- (Recomanat) activar també **Firmar digitalment** per combinar autenticació + confidencialitat :contentReference[oaicite:20]{index=20}

### 6.2 Llegir el correu xifrat
El destinatari obre el correu i Thunderbird:
- Detecta que està xifrat
- Desxifra amb la clau privada (pot demanar contrasenya)
- Mostra que el missatge està **xifrat** i (si toca) **signat** :contentReference[oaicite:21]{index=21}

### 6.3 Comprovar el xifrat sense clau privada
Per demostrar que el contingut no és llegible sense clau:
- Visualitzar el “codi font” / contingut brut del missatge i comprovar que el contingut no apareix en clar (format OpenPGP/MIME). :contentReference[oaicite:22]{index=22}

**Captures (obligatòries):**
- Menú de redacció amb “Xifrar”
- Correu rebut mostrant que està xifrat
- Vista del contingut brut / codi font on es vegi que no està en clar :contentReference[oaicite:23]{index=23}

---

## 7) Part 6 – Proves avançades

### 7.1 Correu signat + xifrat simultàniament
Enviar un correu amb:
- **Xifrar**
- **Firmar digitalment**

Això aporta:
- Autenticació (signatura)
- Integritat (no modificació)
- Confidencialitat (E2EE) :contentReference[oaicite:24]{index=24}

### 7.2 Revocar una clau GPG
Crear certificat de revocació:
gpg --gen-revoke alex1@... > revoke-alex1.asc

perl
Copiar código
Guardar el fitxer en lloc segur. :contentReference[oaicite:25]{index=25}

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
**Important:** fitxer molt sensible; cal guardar-lo xifrat i protegit. :contentReference[oaicite:27]{index=27}

**Captures (obligatòries):**
- Enviament signat + xifrat
- Revocació (comanda + fitxer creat)
- Publicació (ID de clau + intent d’enviament)
- Backup de clau privada (comanda + fitxer) :contentReference[oaicite:28]{index=28}

---

## 8) Qüestions finals

### Qüestió 1: Criptografia asimètrica
a) **Xifrar:** s’utilitza la **clau pública del destinatari** (la pot tenir tothom, perquè es comparteix).  
b) **Desxifrar:** s’utilitza la **clau privada del destinatari** (només la té el destinatari).  
c) **Signar:** s’utilitza la **clau privada del remitent**.  
d) **Verificar signatura:** s’utilitza la **clau pública del remitent**. :contentReference[oaicite:29]{index=29}

### Qüestió 2: Signatura vs Xifrat (taula)
| Característica | Signatura Digital | Xifrat (E2EE) | Signatura + Xifrat |
|---|---|---|---|
| Garanteix confidencialitat | No | Sí | Sí |
| Garanteix autenticació | Sí | No | Sí |
| Garanteix integritat | Sí | No | Sí |
| Pot ser llegit pel servidor | Sí | No | No |
| Requereix clau pública del destinatari | No | Sí | Sí | :contentReference[oaicite:30]{index=30}

### Qüestió 3: TLS vs GPG
a) **SMTP amb STARTTLS:** xifrat **en trànsit** (entre servidors). Els servidors poden llegir el correu quan el desencripten per emmagatzemar-lo.  
b) **GPG/PGP (E2EE):** xifrat **d’extrem a extrem**. Només el destinatari amb la seva clau privada pot llegir el contingut.  
c) **Per què usar tots dos:** TLS protegeix el transport; GPG protegeix el contingut fins i tot si el servidor o el trànsit es veuen compromesos. :contentReference[oaicite:31]{index=31}

### Qüestió 4: Escenaris d’ús
a) Metge → informe mèdic confidencial: **Xifrat + Signatura**  
b) Empresa → factura (no confidencial, però autèntica): **Signatura**  
c) Periodista ← informació sensible d’una font: **Xifrat**  
d) Advocat → contracte legal: **Xifrat + Signatura** :contentReference[oaicite:32]{index=32}

---

## Annex – Llista de captures recomanades
- Part 1: instal·lació, generació i llistat de claus
- Part 2: export/import, trust
- Part 3: import i assignació de clau a Thunderbird
- Part 4: correu signat enviat i verificat
- Part 5: correu xifrat enviat, rebut i contingut brut no en clar
- Part 6: signat+xifrat, revocació, publicació, backup :contentReference[oaicite:33]{index=33}
