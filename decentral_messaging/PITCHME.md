@title[Dezentrales Messenger (XMPP)]
@snap[midpoint]

<h2 style="white-space: nowrap;">Dezentrale Messenger</h2>
<br/>
<h4 style="white-space: nowrap;">The very last word in instant messaging</h4>
(Motto vom XMPP-Client Converations)

@snapend

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
- **Peer-to-Peer**

Geräte tauschen direkt mit einander Nachrichten aus (ohne eine zentrale Componente)

- **Federation**

Mehrere zentrale Komponenten kommunizieren untereinander


Note:
**P2P**
- Postkasten, jeder kann zum Empfänger gehen und selbst etwas in den Kasten werfen.
  (wenn es keine Post gibt)

**Federation**
- E-Mail (ISP: benutzer@hoster.de)
- Telefonnummern (Addr: hat oftmals die ersten Ziffern für sich reserviert)


---

## Dezentralität

#### Warum notwendig?

- Eröffnet ein Wettbewerb
- kleine und viele Angriffsziele
  - vor Hacker
  - vor Regierungen
    - alle Überwachen
    - blockieren / sperren (Zensur)
- Verringert Missbrauch durch Vertrauen

Note:
- _Eröffnet ein Wettbewerb:_ damit Fortschritt für neue Marktteilnehmer
    (Gewinne gehen zum größten Teile in die USA)
   - Entscheidungen: z.B. nur noch auf Englisch, Mark Zuckerberg darf Nachrichten löschen
- _Angriffsziele:_
  - Hacker können nicht alle Server kompromentieren
  - Regierungen können nicht
    - den Zugang zu allen Servern verlangen (NSA - Snowden)
    - alle Server blockieren (Telegram - Russland)
- _Verringert Missbrauch durch vertrauen_
  - **Auswirkung:** nicht alle Daten können **geklaut** oder **analysiert** werden
    - Analysiert zur Manipulation für Werbung oder Politisch (Cambridge Analytics)
  - **Bei Missbrauch** leichterer Wechsel

---

## Dezentralität


#### Nachteile
- Komplexität steigt
- Gewollte Verringerung an Marktanteil

Note:
- _Komplexität steigt:_ Da nicht nur Clients sondern auch Server untereinander sicher (Ausfall, Vertrauensvoll) kommunizieren müssen.

---
## XMPP
- Existiert seit 1999
- IETF Standard seit 2002


- Google Talk 2005 - 2013 (entwickelte Jingle)
- Facebook 2010 - 2014
- WhatsApp nutzt es intern

Note:
- Jingle:
  - Aushandlung von Datenverbindung (angelehnt an SIP)
  - für: Datienaustausch, Video/Voice-Chat, ...

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

Note:

- MUC (Multi User Chat): Gruppenchat

**Als User**

- benutzer@server/gerät

**In MUC**

- chatraum@muc-server/nickame

**Transport**
- ganz unterschiedlich

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


---

## Software <small>Clients</small>
#### Empfehlungen:
- Conversations (Android)
	- Pix-Art Messsenger
- ChatSecure (iPhone)
- Gajim (Desktop)
- ConverseJS (WebClient)
- Viele mehr
	- mit [OMEMO](https://omemo.top)
	- [alle](https://xmpp.org/software/clients.html)

---
## Software <small>Clients</small>
Bombus - Client in J2ME für normale Telefone
<img width="50%" src="img/j2me-bombus.jpg" alt="Wikipedia - Article Java"/>
---

## Software <small>Server</small>
- **prosody** in lua
	- leicht erweiterbar
	- riesige Sammlung an erweiterbaren Modulen (die man nutzen muss)

- **ejabberd** (Fork: mongooseIM) in erlang
	- besitzt alles funktionen von Haus aus
	- sehr gut gewartet

- **OpenFire** in Java

---

## Ist der Hoster gut
Auswahl des richtigen Servers
- [Compliance](https://compliance.conversations.im/) ([support Alles](https://compliance.conversations.im/api/compliant_servers/) / API)
- [Status](https://status.conversations.im/historical/) für S2S + Uptime

XEPs:
- PEP / PubSub
- MAM (für MUC)
- HTTP-Upload
- DNS-SRV for TLS (HTTPS)

Note:
- Personal Eventing Protocol: Geolocation, Mood, Activity, Tune
- Message Archive Management:
  - Vorteil gegenüber: Threema und WhatsApp (mit OMEMO auch gegenüber Telegram)
  - OMEMO: Neue Geräte können alte Nachrichten nicht entschlüsseln
- HTTP-Upload: Offline und in MUC Datenaustausch
- "umgeht" Firewalls

---
## XMPP

### Verschlüsselung
- Off-The-Record
- OpenPGP
- OX
- OMEMO

Detailert: [here](https://conversations.im/omemo)

Note:
- Neben TLS (SSL)

---
## XMPP <small>Verschlüsselung</small>

- Geräte erstellt **asynchrones** Schlüsselpaar
  - öffentlichen Schlüssel wird per PubSub auf dem Server hinterlegt
- Kontakte werden durch PEP / PubSub über neuen Schlüssel informiert
  - Dieser muss diesen öffentlichen Schlüssel

Note:
- synchrone: entspricht ein allen bekanntes Passwort
  - asynchrone: mathematisches Verfahren mit öffentlicher und privater Schlüssel
- Kontakte = Roster
- den **neuen oder weiteren** öffentlichen Schlüssel

- Signiert und Verschlüsselt
- zurückziehen des Schlüssels


---

@snap[midpoint]
<h1>Demo</h1>
[Anleitung](https://media.kuketz.de/blog/artikel/2016/conversations/Anleitung_Conversations_V1.1_CC-BY-SA.pdf)
@snapend
---

## Ausblick

- Transports
  - Biboumi: IRC
  - Spectrum2: e.g AIM, ICQ, MSN, Yahoo, Telegram, Twitter, "WhatsApp"
- Commands
	- Internet of Thinks

[XEP-Liste](https://xmpp.org/extensions/) letzter Eintrag: XEP-0410: MUC Self-Ping (Schrödinger's Chat)

Note:
- Transport WhatsApp Warnung, vor Protokolländerungen und Sperrungen

---

## Alternativen zu XMPP

#### Peer-to-Peer
- Nutzen das Tor netzwerk
	- **Tox**
	- **Briar**
		- kann auch Local per Wifi und Bluetooth arbeiten
	- ... (viele mehr)
- libp2p

- (mir sonst keine Weiteren bekannt ...)

---

## Alternativen zu XMPP

#### Federation
- **Matrix** (Riot):
	- Protokoll durch einer Firma vorgegeben
	- IRC (Transport) representiert oftmals alle Benutzer, als ein Einziger
- (mir sonst keine Weiteren bekannt ...)


---

@snap[midpoint]
<h1>Ende</h1>
<a href="https://www.ccc.de/de/hackerethik"><h4>Hackerethik</h4></a>

3. **Mißtraue Autoritäten – fördere Dezentralisierung.**
@snapend

