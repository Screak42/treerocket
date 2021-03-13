---
layout: default
---

<!-- MENU BEGINN -->

<ul style="text-align: center;">
   {% for item in site.data.samplelist.docs %}
   <a href="{{ item.url }}">{{ item.title }}</a>
   |   {% endfor %}
</ul>

* * *

<!-- MENU END -->

[2021.01.09]

// posted 2021.01.09 https://github.com/Screak42/treerocket/edit/gh-pages/blog.md

\[2021.01.09\]

# Was ist lost mit Whatsapp

Jetzt, in 2021 wird Whatsapp seine Richtlinen ändern. Wie von vielen schon vor Jahren vorausgesagt, wird Whatsapp in Zukunft Daten mit Facebook teilen. Mit dem in Europa aktiven [GDPR](https://de.wikipedia.org/wiki/Datenschutz-Grundverordnung) ändert sich für Europäische Nutzer (noch?) nicht sehr viel; zumindest laut Gesetz.

Dass man sich darauf KEINESfalls verlassen sollte haben wir insbesondere bei Unternehmen wie Facebook ja schon mehrfach erfahren. Im Zweifelsfall entschuldigt sich der Herr Zuckerberg dann halt noch mal, schaut ein bisschen traurig und schon haben (erneut) alle vergessen was passiert ist.
Verstehen kann ich persönlich das plötzliche Geschrei um Whatsapp überhaupt nicht - das ganze ist seit dem Verkauf von Jan Koum an Facebook meiner Meinung nach fragwürdig. (Unabhängig von Jans Statements)

Whatsapp hat Deutschland fest in der Hand klingt dramatisch, ist aber der Fall. Fast jeder der ein “Smartphone” hat, hat es; viele möchten es loswerden, “können” aber nicht wegen der vielen Kontakte. “Elterngruppen”, Häkelgruppen, Buchclub o.ä. … teilweise sicher verständlich, aber wohl auch überbewertet - und irgendwer muss mal den Anfang machen. Warum “die Leute” so resistent sind und es so ein Drama zu sein scheint auf einen anderen Messenger umzusteigen ist mir unverständlich - aber scheinbar ist es ein Problem für viele.

###### Übliche Gründe sind weil man Whatsapp nicht verlassen kann:

- Alle meine Freunde haben es
- Ich habe nichts zu verbergen
- Die wissen doch eh schon alles
- Andere sind auch nicht besser
- Ich bin in Gruppen
- Ich möchte Nachrichten an mehrere Personen senden
- Mein Chef benutzt es

Auch wenn heutzutage viele Leute bereit sind ihr Privatleben über ein Megaphon auf die Strasse zu plärren (z.b. Twitter/Instagramm/Facebook) um allen zu erzählen das Hasso schon bei Fuss laufen kann, sollte man kurz darüber nachdenken womit man diese Dienste bezahlt. Es geht also um das Geschäftsmodell des jeweiligen Anbieters.

In der Regel tut man das in irgend einer Form mit seinen persönlichen Daten. Üblicherweise hört man an dieser Stelle “Ich habe nichts zu verbergen” oder “die wissen doch eh schon alles” - darum geht es jedoch kein bisschen. Wäre dass so, hätten die Benutzer ja auch alle nichts dagegen wenn jemand bei Ihnen im Klo und/oder Schlafzimmer eine Kamera aufstellt.
Abgesehen davon dass die Aussage völliger blödsinn ist, haben 99% der Bevölkerung nicht die geringste Vorstellung was Unternehmen die Ihr Geld in erster Linie mit Werbung, Benutzerverhalten und deren Analyse verdienen mit den abgreifbaren Daten überhaupt anzufangen wissen. Eine sehr oberflächliche, grobe Übersicht gibt es hier:

![Data Linked to you Vergleich](/assets/images/2021.01.09.priv.share.jpg) (Source: https://bgr.com/wp-content/uploads/2021/01/app-privacy-labels-facebook-messenger-imessage-signal-whtasapp.jpg)

Gehen wir kurz mal davon aus dass die Verschlüsselung bei Whatsapp wirklich keine Hintertür hat (da die Software “closed source” ist lässt sich das nicht verlässlich prüfen) - Nachrichten also nicht im Klartext auf den Servern oder gar vorher im Klartext mitgelesen werden können.
Ich spreche hier auch erstmal nicht von Ende-zu-Ende Verschlüsselung.
Wir müssen uns hier auch bewust sein dass es zusätzlich zu Ende-zu-Ende-Verschlüsselung auch noch "Peer-to-Peer-Data" gibt. Es ist also durchaus möglich einen Chat nur zwischen 2 Punkten stattfinden zu lassen, ohne dass die Daten über einen Server fliessen. Das ist äusserst komplex und wenigstens für die Kontaktaufname selbst wird irgendwo ein Server benötigt.

Bleiben wir aber bei Whatsapp und der Ende-zu-Ende Verschlüsselung.
Ich persönlich glaube daran nur sehr begrenzt, ganz besonders wenn es um Gruppen-chats geht. Mein Zweifel darin ist durchaus begründet - und zwar in erster Linie technisch. Als “Nicht Programmierer” oder “Nicht-Cryptographie-Enthusiast” hat man verständlicherweise auch wenig Vorstellung wie komplex das Thema überhaupt ist - auch heute noch. Setzen wir voraus, das die generierung der Schlüssel auf Seiten des jeweiligen Benutzers problemlos und individuell von statten geht (was nicht nötigerweise der Fall und so einfach ist)…

Für eine Verschlüsselung werden “Schlüssel” von allen Parteien benötigt. Ohne dass zwischen allen (!) Parteien die Schlüssel entsprechend ausgetauscht wurden ist eine Ende-Zu-Ende Verschlüsselung unmöglich. Beim Beitreten einer Whatsapp Gruppe sieht man üblicherweise die komplette Historie - auch alles was vor dem Beitreten stattfand. D.h. möglicherweise (höchstwarscheinlich sogar) besteht eine Speicherung und auch Verschlüsselung AUF dem Server (also BEI Whatsapp), aber höchstwarscheinlich nicht Ende-zu-Ende. 
D.h. die Inhalte in Gruppenchats sind wenigstens dem Whatsapp Betreiber Facebook bekannt. Durchaus möglich, und sogar sehr warscheinlich das diese Daten verschlüsselt gespeichert werden, heisst aber nicht dass Facebook die Schlüssel unbekannt sind. 
(Unmöglich zu sagen, da die Software ja closed source ist)

Wer darüber aber überhaupt nachdenkt sollte aus offensichtlichen Gründen ohnehin keinerlei Probleme haben Whatsapp den Rücken zu kehren. 

In jedem Fall hinterlässt jeder Nutzer einen unvorstellbaren Haufen an Spuren und Daten die insbesondere für Unternehmen wie Facebook durchaus enorm wertvoll sind. Die Rede ist hier nicht nur von so offensichtlichen Daten wie:

- IP-Adresse
- Standort
- Software-Version
- Betriebssystem

Es geht hier zusätzlich um:

- Nutzungsdauer (und wann und wie oft)
- Foto-Header-Informationen
- Gruppenaktivitäten (Selbst wenn wir davon ausgehen dass Inhalte verschlüsselt sind, weiss Whatsapp wenigstens dass Benutzer A in 12 Gruppen aktiv ist, und "wie" aktiv die jeweiligen Benutzer sind)
- Avatar-Bild-Informationen
- Kontakte
- Wifi- oder Mobil-Daten Informationen, Nutzungsdauer, Netzwerknamen, eventuell IMEI
- “Diagnose” Was Diagnose genau bedeutet kann vielschichtig sein, da die Software closed source ist, kann Facebook behaupten was immer sie möchten. Das nachzuprüfen ist denkbar schwierig.

Aus all diesen Daten lassen sich individuell Rückschlüsse ziehen, das nennt sich heutzutage “Fingerprinting”. Zusätzlich lassen sich diese Daten problemlos mit anderen Benutzern vergleichen und - sind wir mal ehrlich wir reden hier über Facebook. Und - dafür ist nicht zwingender-weise ein Facebook Account notwendig. Facebook ist in unzählige Webseiten integriert, auch wenn nicht von allen genutzt, lässt sich über sogenanntes Browser-Fingerprinting, Cookies und Cross-Site-Scripting ein sehr präzises Benutzerprofil erstellen. (Cookies sind dazu nicht zwindenderweise nötig, bieten aber wesentlich grössere Möglichkeiten.)

In vielen Fällen sogar so präzise dass aus den vielen Millionen Nutzern Analysegruppen von nur wenigen hundert; nicht unmöglicherweise weniger entstehen. (Das ganze auf individuelle Personen herunterzubrechen ist durchaus möglich; rechtlich allerdings fragwürdig. Das heisst natürlich wiederum überhaupt nicht dass es nicht betrieben wird) D.h. zusammengefasst dass “Facebook” im Weitesten Sinne ganz genau feststellen kann wer, wann, wo, wie oft, was tut und mit wem. Ich sehe dieses Problem insbesondere bei Diensten die einer Firma wie Facebook gehören, die hauptsächlich Geld mit Benutzerdaten, Werbung und dem Verkauf von Benutzeranalysen verdienen.

Dabei endet dieses Datenschutz-Desaster aber noch lange nicht, besonders bei Firmen wie Facebook geht es hier erst richtig los. Denn diese Daten werden mehr oder weniger unkontrolliert mit dritten-, vierten, oder gar mehr Parteien geteilt. Laut GDPR ist das ohne Zustimmung nicht zulässig, kontrollieren kann man dies als Benutzer schlecht bis gar nicht - und wird in der Praxis betrieben.

Alternativen gibt es; und niemand wird irgendwelche Features missen müssen - manche sehen eventuell etwas anders aus, im grossen und ganzen ist es das gleiche. Natürlich ist die Frage wen man denn heutzutage noch vertrauen soll - Die Antwort darauf ist lang, komplex und individuell. Wer sich diese Frage allerdings stellt, ist auf dem richtigen Weg. Wichtig ist allerdings auch, sich seine EIGENE Meinung zu bilden und nicht irgendeinem “Messenger-bashing” zu glauben. Es ist sicher davon auszugehen, je besser die Verschlüsselung, je weiter weg ein Dienst von üblichen Überwachungs-Szenarien ist, desto mehr fragwürdige Benutzer wird es geben. Das heisst aber nicht dass dies einen negativen Einfluss auf den Dienst hat. Es gibt Milliarden von Virenverseuchten Webseiten, Seiten die ausschliesslich auf Betrug ausgelegt sind … deswegen zu behaupten das “Internet” wäre ausschliesslich böse ist einfach albern, naiv und falsch.

Dezentralisierte, verschlüsselte, Open-Source Lösungen, die keine Telefonnummer oder andere persönliche Daten abfragen wären die optimale Antwort. Aber bleiben wir realistisch, es muss so einfach wie möglich zu benutzen sein und es muss für die grosse Masse dennoch einfach sein, seine Kontakte zu finden. Das funktioniert bei vielen leider nach wie vor über eine Telefonnummer.

Für mich ist wichtig dass ich Chat-clients auf dem Computer sowie mobilen Geräten (Tablet / Telefon) zur verfügung habe.

- Matrix (als client verwende ich Element)
- Telegram

Andere populäre Alternativen (neben unzähligen ungenannten)

- Signal (Momentan sicherlich in Ordnung, erlebt gerade einen enormen Ansturm an neuen Nutzern. Das kann langfristig meiner Meinung nach zu Problemen führen, ist ohne Frage aber eine hervorragende Alternative)
- Threema (Kostenpflichtig, Desktop client nur über Browser)
- Discord (Das “Gamer-Chat-Netzwerk”) Vom Datenschutz her das fragwürdigere, aber immer noch besser als Whatsapp.

Bedauerlicherweise ist Whatsapp trotz allem und nach wie vor besonders in Deutschland enorm populär. Der Ursprung ist vermutlich dass es einer der ersten “grossen” Messenger Dienste war die nahezu jedem mit einem Mobiltelefon Nachrichtenaustausch ausserhalb der teuren SMS Dienste und “Cross Platform” erlaubte. Das betrifft meiner Erfahrung nach hauptsächlich eine bestimmte Generationengruppe.

“Damals” kostete die App knapp einen Euro pro Jahr um den Dienst zu nutzen - bis irgendwann Facebook das Unternehmen aufkaufte… und wir wissen es alle; nichts im Leben ist kostenlos. Im Falle von Whatsapp bezahlen wir es halt mit persönlichen Informationen.

[Whatsapp Privacy Policy](https://www.whatsapp.com/legal/updates/privacy-policy/?lang=de) [Whatsapp FAQ](https://faq.whatsapp.com/general/security-and-privacy/how-we-work-with-the-facebook-companies)

- [Matrix Chat (ehemals Riot)](https://matrix.org/) als Client empfohlen [Element](https://element.io/)
- [Telegram](https://telegram.org/)
- [Threema](https://threema.ch/en)
- [Discord](https://discord.com/)

Wer generell auf der Suche nach Informationen in diesem Bereich ist, findet unter [Privacytools](https://www.privacytools.io/) nützliche Informationen für den Anfang.
