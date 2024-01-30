# Cinc fases 
1. Reconeixement
- Pasiva sense interaccio
- Activa amb interaccio
- Eines: nmap, maltego, shodan
----------
2. Escaneig
- Ports
- Vulnerabilitats
- Xarxa
- Eines: nessus, wireshark, OpenVAS
----------
3. Acces
- Força bruta
- Explotacio vulnerabilitats
- Injeccio SQL
- Eines: Hydra, Metasploit, SQLmap
----------
4. Manteniment d'acces
- Keylogger
- Backdoors
- Eines: Meterpreter, Netcat
----------
5. Esborrat d'empremtes
- Eliminar logs
- Tecniques d'evasio
- Eines: Ccleaner, LogWiper, BleachBit
----------
# SERVEI DNS
- conusltes/respostes DNS
- actualitzacions dinamiques
- transferencies de zona
- notificacions
----------
- BASE: SO, bind, xarxa
- DADES: Parametres, registres de zona, transaccions

vuln:
1. Locals
2. Serv-Serv
3. ServMaster-Esclau
4. ServMaster-ClientCache
5. Serv-Client

- Man in the middle: Interposarte en la comunciacio entre dues parts.
- DNS tunneling: Enviar dades no-DNS de punt a punt.
- Dos: Denegar el servei d'un sobre carrec.
- IP Spoofing: Falseijar IP l'origen als paquets enviats a la victima. 

sol:
- DNSSEC: Una capa de seguretat per damunt del DNS que xifra les dades amb signatures i claus per asegurar la integritat i autenticitat.
- DNS sobre TLS (port 853) confidencialitat i integritat
- DNS sobre HTTPS (port 443) privadesa i encriptacio

# DNS

| SECCION     | Descripción |
|-------------|--------------------------------------------------------------------|
| HEADER      | Contiene información sobre el tipo de mensaje. Incluye campos que informan sobre el número de entradas en otras secciones del mensaje. |
| QUESTION    | Contiene una o más solicitudes de información (queries) que se envían al servidor DNS. |
| ANSWER      | Contiene uno o más registros que responden a la(s) solicitud(es). |
| AUTHORITY   | Contiene uno o más registros que apuntan al servidor autoritativo del dominio en cuestión. |
| ADDITIONAL  | Registros con información adicional no necesaria para responder a la query. |

# SERVEI FTP
- transferir fitxers
- port 20 (dades) i port 21 (comandes)
- usa la capa 5

vuln:
1. Login-Password (no garanteix qui pot ser)
2. Contrasenyes en text clar
3. No xifra la sessio FTP
- força bruta
- rebot FTP
- Extra (massa admins, mala config, serv no actualitzat, falta d'alertes)

sol:
- SCP (xifra informacio transferida amb SSH)
- SFTP (com FTP pero xifrat amb SSH)
- FTPS (proteigeix credencias i dades amb TLS)
	1. Explicit (negociacio del xifratge)
	2. Implicit (xifratge per defecte)
- Llista blanca (permet) i Llista negra (bloqueija)
- Extra (contrasenyes fortes, limitar admins, desabilitar anon, permisos)

FTP Actiu: 
	1. Canal de Comandes: Client (port aleatori) → Servidor (port 21).
	2. Canal de Dades: Servidor (port aleatori) → Client (port 20).
FTP Pasiu (millor per al client): 
	1. Canal de Comandes: Client (port aleatori) → Servidor (port 21).
	2. Canal de Dades: Client (port aleatori) → Servidor (port aleatori).

# SERVEI CORREU ELECTRONIC

vuln:
- Phishing: enganyar els destinataris per capturar informacio confidencial
- Spoofing: falsificacio i suplantació d'indentitat

sol:
- SPF: verificar que pertanyen a un domini o IP autoritzat
- DKIM: verificar que no s'aguin moficiat els correus durant el transit
- DMARC: combina SPF i DKIM per validar l'origen de correus
- OpenPGP: estandard de codi obert per akl xifratge i signatura digital
	1. Comprova l'autenticitat i integritat
	2. Xifra el contingut del correu
- Extra (antimalware, precaucio, combrovar domini [whois], separar personal i corporatiu)

# SERVEI WEB
- Service Provider: Ofereix i implementa el servei web.
- Service Broker: Intermediari entre el proveïdor i el sol·licitant del servei.
- Service Requester: Descobrix qui és el proveïdor utilitzant el protocol WSDL.

1. WSDL (Web Services Definition Language)
	- basat en XML
	- format dissenyat per ser interpretat per una màquina, no humans
	- inclou detalls com operacions, missatges i protocols suportats pel servei web.
2. SOAP (Simple Object Access Protocol)
	- basat en XML
	- disposa d'un esquema XML determinat.
	- format dels missatges, les regles d'intercanvi de missatges, gestió d'errors, etc
	1. SOAP Envelope: element arrel que identifica el missatge com un missatge SOAP.
	2. SOAP Header: informació sobre autenticació, codificació de dades, i instruccions sobre com processar el missatge.
	3. SOAP Body: la informació principal a ser intercanviada entre les aplicacions.
	4. SOAP Fault: conté informació sobre errors en cas que es produeixin.

vuln:
- Divulgacio WSDL: arxius WSDL d'un servei web estan exposats o accessibles públicament.
- Bomba XML: documents XML maliciosament dissenyats per consumir recursos del sistema.
- Injecció XPath: vulnerabilitats al codi de consultes XPath, inserint dades malicioses.
- Injecció XML: quan un atacant pot inserir contingut XML maliciós en un sistema

sol:
- Restringir l'acces als arxius
- Limitar la mida i la complexitat dels documents XML processats.
- Validar i sanejar totes les entrades dels usuaris.
- Validar tot el contingut XML contra un esquema conegut i segur.

# SERVEI VoIP
- Terminals: Dispositius finals utilitzats per a la comunicació
- Gateways: Ponts entre la xarxa de telefonia tradicional i la xarxa IP.
- Gatekeepers: Gestiona connexió i l'autorització d'accés en xarxes VoIP basades en H323.

Avantatges
	1. Cost Reduït: 
	2. Flexibilitat: fer i rebre trucades des de qualsevol lloc amb accés a Internet.
	3. Altres Serveis: Facilita la integració amb altres serveis basats en IP.
Inconvenients
	1. Dependència: Requereix una connexió a Internet estable i de bona qualitat.
	2. Latència: Pot experimentar retards o variacions en la transmissió de veu.
	3. Seguretat: Pot ser més susceptible a atacs cibernètics.

Protocols:
	- RTP: Maneja la lliurament de dades en temps real, com ara l'àudio i vídeo.
	- RTCP: Conjunt amb RTP per proporcionar informació de control i monitorització.
	- H323: Un dels primers protocols estàndards utilitzats en VoIP.
	- SIP: Protocol ampliament utilitzat per a sessions interactives de comunicació.

vuln:
- Dos
- Accesos desautoritzats
- Spoofing
- Eavesdropping: Intercepció i escolta de converses privades.
- Fuzzing: Enviaments de dades aleatòries o malformades per provocar errors o fallades.

sol:
- TLS: Capa de seguretat addicional mitjançant l'encriptació de les comunicacions.
- VPNs: Canals segurs de comunicació a través d'Internet o altres xarxes públiques.
- Protocol SRTP: Extensió del RTP que proporciona xifratge, autenticació i integritat.
- VLANs: Separar el tràfic de VoIP del tràfic de dades general de la xarxa.
- Limitar l'Accés a la Xarxa VoIP i Volum de Dades
