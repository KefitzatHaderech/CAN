# 1. Einführung

## 1.1. Motivation für CAN

Die neueren Entwicklungen in der Automobilindustrie sind geprägt von einer verstärkten Integration von Elektronik. Die Haupttreiber dafür sind vor allem die immer anspruchsvolleren Anforderungen der Kunden an moderne Fahrzeuge. Gleichzeitig werden die gesetzlichen Vorgaben zur Abgasemission zunehmend verschärft. Die Globalisierung trägt ebenfalls dazu bei, indem sie einen verstärkten Wettbewerbs- und Kostendruck ausübt und somit kontinuierlichen Innovationsdruck erzeugt.

In den Anfängen waren eigenständig arbeitende elektronische Steuergeräte ausreichend, um elektronische Funktionen umzusetzen. Doch schon früh erkannte man, dass die Koordination dieser Steuergeräte die Fahrzeugfunktionalität erheblich verbessern könnte. Der Datenaustausch zwischen den elektronischen Steuergeräten erfolgte anfangs auf konventionelle Weise, indem jedem zu übertragenden Signal ein physischer Kommunikationskanal zugeordnet wurde.

<imgsrc="image/1705580627420.png"alt="drawing"width="600"/>

Der zunehmende Verkabelungsaufwand führte jedoch zu begrenzten Möglichkeiten des Datenaustauschs. Als Lösung für dieses Problem kam nur der bitserielle Austausch von Daten über einen einzigen Kommunikationskanal (Bus) infrage. Dadurch entstand die Notwendigkeit, ein speziell auf die Anforderungen des Automobils zugeschnittenes serielles Kommunikationssystem zu entwickeln.

Bereits Anfang der 80er Jahre begann Bosch mit der Entwicklung eines solchen seriellen Kommunikationssystems, dem sie den Namen CAN (Controller Area Network) gaben. Auch heute noch spielt CAN eine entscheidende Rolle bei der Vernetzung von elektronischen Steuergeräten im Antriebs-, Fahrwerks- und Komfortbereich von Fahrzeugen. Besonders hervorzuheben ist die sehr sichere Datenübertragung, die den Echtzeitanforderungen der jeweiligen Einsatzgebiete gerecht wird.

Seit der Einführung von CAN gehören komplexe und unterschiedlich gestaltete Kabelbäume in Fahrzeugen der Vergangenheit an. CAN erleichtert nicht nur die Planung und Installation, sondern reduziert auch das Gewicht und den Platzbedarf für die Verkabelung erheblich.

## 1.2. Standardisierung

Die CAN-Technologie wurde im Jahr 1994 standardisiert und ist hauptsächlich durch drei ISO-Dokumente definiert. Die ISO 11898-1 beschreibt dabei das CAN-Protokoll. Im Gegensatz zum Referenzmodell für Datenkommunikation umfasst das CAN-Protokoll lediglich den Data Link Layer (MAC - Medium Access Control, LLC - Logical Link Control) und das Physical Layer (PLS - Physical Signalling).

Die Implementierung des CAN-Protokolls erfolgt in Hardware. Es gibt mittlerweile eine Vielzahl von CAN-Controllern, die sich im Wesentlichen nur im Umgang mit CAN-Nachrichten unterscheiden, was sich in Unterschieden auf der Object Layer auswirkt. Man unterscheidet CAN-Controller mit Objektespeicherung (sogenannte Full-CAN-Controller) von CAN-Controllern ohne Objektespeicherung (sogenannte Basic-CAN-Controller).

Die beiden ISO-Dokumente ISO 11898-2 und ISO 11898-3 decken die beiden Unterschichten PMA (Physical Medium Attachment) und PMS (Physical Medium Specification) des Referenzmodells für Datenkommunikation ab. Sie beschreiben zwei verschiedene CAN Physical Layer: CAN-High-Speed Physical Layer und CAN-Low-Speed Physical Layer. Die Hauptunterschiede liegen in der Spannungsdefinition und der Datenübertragungsgeschwindigkeit (Datenrate).

Die ISO 11898-3 ermöglicht Datenraten von bis zu 125 KBit/s und findet daher hauptsächlich Anwendung im Komfortbereich des Automobils. Die ISO 11898-2 erlaubt Datenraten bis zu 1 MBit/s und wird daher vor allem im Antriebs- und Fahrwerksbereich des Automobils eingesetzt (bezüglich der Datenübertragung in einem CAN-High-Speed CAN-Netzwerk beschreibt die ISO 11898-5 das Verhalten eines CAN-Knotens im "Low Power Mode").

Für die Unterschicht MDI (Medium Dependent Interface) des Physical Layers existiert kein Standard. Die CiA DS-102 (CiA: CAN in Automation) empfiehlt lediglich die Verwendung bestimmter Stecker (SUB-D9). Es wird auch empfohlen, eine bestimmte Steckerbelegung einzuhalten.

Die ISO 11898-1 definiert eine ereignisgesteuerte Kommunikation. Bei hoher Buslast kann es insbesondere bei niedrig priorisierten CAN-Nachrichten zu Verzögerungen kommen. Um eine deterministische Kommunikation in einem CAN-Netzwerk sicherzustellen, steht die ISO 11898-4 zur Verfügung. Diese ist eine Erweiterung des Data Link Layers und bietet eine Time Triggered Communication-Option für CAN-basierte Netzwerke.

Die untenstehende Grafik "Standard und Implementierung" zeigt den Zusammenhang zwischen dem ISO/OSI-Referenzmodell für Datenkommunikation, dem CAN-Standard und der Implementierung.

<imgsrc="image/1705581663183.png"alt="drawing"width="600"/>
