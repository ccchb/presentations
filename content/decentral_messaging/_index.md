---
title: "Dezentrale Messenger"
outputs:
  - "Reveal"
---

<h2 style="white-space: nowrap;">Dezentrale Messenger</h2>
<br/>
<h4 style="white-space: nowrap;">The very last word in instant messaging</h4>
(Motto vom XMPP-Client Converations)

<span class="text-reboot">genofire - Chaos Computer Club Bremen e.V.</span>

---

## Agenda
- Dezentralität
- XMPP - Der Standard
- Software (Client und Server)
- Ist der Hoster gut
- Verschlüsselung
- Ausblick
- Alternativen

---

## Dezentralität
- **Federation**

Kommunikation über verschieden unabhängige zentrale Komponenten

<img src="./img/federation.svg" style="border: none; background:transparent;" />

{{% note %}}
**Federation**
- E-Mail (ISP: benutzer@hoster.de)
- Telefonnummern (Addr: hat oftmals die ersten Ziffern für sich reserviert)
{{% /note %}}

---

## Dezentralität
- **Peer-to-Peer**

Geräte tauschen direkt miteinander Nachrichten aus (ohne eine zentrale Componente)

<img src="./img/p2p.svg" style="border: none; background:transparent;" />

{{% note %}}
**P2P**
- Postkasten, jeder kann zum Empfänger gehen und selbst etwas in den Kasten werfen.
  (wenn es keine Post gibt)
{{% /note %}}

---

## Dezentralität

#### Warum notwendig?

- Eröffnet ein Wettbewerb
- kleine und viele Angriffsziele
  - vor Kriminelle
  - vor Regierungen
    - alle Überwachen
    - blockieren / sperren (Zensur)
- Verringert Missbrauch durch Vertrauen

{{% note %}}
- _Eröffnet einen Wettbewerb:_ damit fortschritt
    (Gewinne gehen zum größten Teile in die USA)
   - Entscheidungen: z.B. nur noch auf Englisch, Mark Zuckerberg darf Nachrichten löschen
- _Angriffsziele:_
  - Hacker können nicht alle Server kompromentieren
  - Regierungen können nicht
    - den Zugang zu allen Servern verlangen (NSA - Snowden)
    - alle Server blockieren (Telegram - Russland)
- _Verringert Missbrauch durch Vertrauen_
  - **Auswirkung:** nicht alle Daten können **geklaut** oder **analysiert** werden
    - Analysiert zur Manipulation (Werbung oder politisch, siehe Cambridge Analytica)
  - **Bei Missbrauch** leichterer Wechsel
{{% /note %}}

---

## Dezentralität


#### Nachteile
- Komplexität steigt
- Gewollte Verringerung an Marktanteil
- Kann auch von kriminellen Elementen genutzt werden
- Nutzer müssen ggf. sich Ihre Adresse und Passwort merken

{{% note %}}
- _Komplexität steigt:_ Da nicht nur Clients, sondern auch Server untereinander sicher (Ausfall, vertrauensvoll) kommunizieren müssen.
- _kriminellen Elementen:_ wie bei jeder Technologie kann diese auch von Bösen genutzt werden.
- _... sich merken:_ allerdings müssen Sie dies auch für Ihre E-Mail-Adresse, was noch Standard im Internet ist.
{{% /note %}}

---
### Extensible Messaging and Presence Protocol (XMPP)

- Existiert seit 1999 (unter den Namen Jabber)
- IETF Standard seit 2002


- Google Talk 2005 - 2013 (entwickelte Jingle)
- Facebook 2010 - 2014
- WhatsApp nutzt es intern

{{% note %}}
- Jingle:
  - Aushandlung von Datenverbindung (angelehnt an SIP)
  - für: Datenaustausch, Video/Voice-Chat, ...
{{% /note %}}

---

## XMPP
#### Adressierung
JID (Jabber ID) genannt:
```
node@domain/ressource
```

URI-Format: (falls MUC mit `?join` am Ende)

```
xmpp:node@domain?join
```

{{% note %}}
- MUC (Multi User Chat): Gruppenchat

**Als User**

- benutzer@server/gerät

**In MUC**

- chatraum@muc-server/nickame

**Transport**
- ganz unterschiedlich
{{% /note %}}

---
## XMPP

**Message**

```xml
<message from="geno@fireorbit.de"
 to="#ccchb@irc.hackint.org" type="groupchat">
	Hello World
</message>
```

Types:

- chat
- groupchat
- headline
- normal
- error

---
## XMPP

**Present**: Aktuelle Live Informationen

```xml
<present to="#ccchb@irc.hackint.org" type="subscribe">
</present>
```

Types:

- error
- probe
- subscribe(d)
- unavailable
- unsubscribe(d)

---
## XMPP

**IQ** (Instant Query): Abfragen mit Rückantworten

```xml
<iq to="irc.hackint.org" type="get">
	<ping xmlns='urn:xmpp:ping'/>
</iq>
```

Types:

- get
- set
- result
- error

{{% note %}}
- Die Inhalte, die in diesen XML-Elementen drin sind, werden im RFC nicht vorgegeben und kann für viele Funktionen genutzt werden.
{{% /note %}}

---

## Software <small>Clients</small>
#### Empfehlungen:
- Conversations (Android)
	- Pix-Art Messenger
- ChatSecure (iPhone)
- Gajim (Desktop)
- ConverseJS (WebClient)
- Viele mehr
	- mit [OMEMO](https://omemo.top)
	- [alle](https://xmpp.org/software/clients.html)

---

## Software <small>Clients</small>
Bombus - Client in J2ME für normale Telefone
<center>
  <img width="50%" src="img/j2me-bombus.jpg" alt="Wikipedia - Article Java"/>
</center>

---

## Software <small>Server</small>
- **prosody** in lua
	- leicht erweiterbar
	- riesige Sammlung an erweiterbaren Modulen (die man nutzen muss)

- **ejabberd** (Fork: mongooseIM) in erlang
	- besitzt alle nötigen Funktionen von Haus aus
	- sehr gut gewartet

- **OpenFire** in Java

---

## Ist der Hoster gut
Tools zum Testen des Servers (Auswahl an Servern)

- [Compliance](https://compliance.conversations.im/) ([support Alles](https://compliance.conversations.im/api/compliant_servers/) / API)
- [Status](https://status.conversations.im/historical/) für S2S + Uptime

XEPs:

- PEP / PubSub
- MAM (für MUC)
- HTTP-Upload
- DNS-SRV for TLS (HTTPS)

{{% note %}}
- Personal Eventing Protocol: Geolocation, Mood, Activity, Tune
- Message Archive Management:
  - Vorteil gegenüber: Threema und WhatsApp (mit OMEMO auch gegenüber Telegram)
  - OMEMO: Neue Geräte können alte Nachrichten nicht entschlüsseln
- HTTP-Upload: Offline und in MUC Datenaustausch
- "umgeht" Firewalls
{{% /note %}}

---
## XMPP

### Verschlüsselung
- Off-The-Record
- OpenPGP
- OX
- OMEMO

Detailert: [here](https://conversations.im/omemo)

{{% note %}}
- Neben TLS (SSL)
{{% /note %}}

---

## XMPP <small>Verschlüsselung</small>

- Geräte erstellt **asynchrones** Schlüsselpaar
  - öffentlichen Schlüssel wird per PubSub auf dem Server hinterlegt
- Kontakte werden durch PEP / PubSub über neuen Schlüssel informiert
  - Dieser muss diesen öffentlichen Schlüssel laden

{{% note %}}
- synchrone: Entspricht einem Passwort, was allen Gesprächsteilnehmern bekannt ist.
  - asynchrone: mathematisches Verfahren mit Schlüsselpaaren (öffentlicher und privater Schlüssel)
- Kontakte = Roster
- den **neuen oder weiteren** öffentlichen Schlüssel

- Signiert und verschlüsselt
- zurückziehen des Schlüssels
{{% /note %}}

---

<center>
<h1>Demo</h1>
[Anleitung](https://media.kuketz.de/blog/artikel/2016/conversations/Anleitung_Conversations_V1.1_CC-BY-SA.pdf)
</center>

---

## Ausblick

- Transports
  - Biboumi: IRC
  - Spectrum2: e.g AIM, ICQ, MSN, Yahoo, Telegram, Twitter, "WhatsApp"
- PubSub
  - Blogging / Posting (siehe Movim)
- Commands
  - Internet of Things

[XEP-Liste](https://xmpp.org/extensions/) letzter Eintrag: XEP-0410: MUC Self-Ping (Schrödinger's Chat)

{{% note %}}
- Transport WhatsApp Warnung, vor Protokolländerungen und Sperrungen
{{% /note %}}

---

## Alternativen zu XMPP

#### Peer-to-Peer
- Nutzen das Tor-Netzwerk
	- **Tox**
	- **Briar**
		- kann auch Local per Wifi und Bluetooth genutzt werden
	- ... (viele mehr)
- libp2p

- (mir sonst keine Weiteren bekannt ...)

---

## Alternativen zu XMPP

#### Federation
- **Matrix** (Riot):
	- Änderungsvorschläge am Protokoll werden durch das Unternehmen entschieden
- (mir sonst keine Weiteren bekannt ...)


---

<center>
  <h1>Ende</h1>
  <a href="https://www.ccc.de/de/hackerethik"><h4>Hackerethik</h4></a>

  **3. Mißtraue Autoritäten – fördere Dezentralisierung.**
</center>
