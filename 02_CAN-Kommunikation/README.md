## 2. CAN-Kommunikation

### 2.1. CAN-Netzwerk

Ein CAN-Netzwerk besteht aus mehreren CAN-Knoten, die über einen physischen Übertragungskanal, den sogenannten CAN-Bus, miteinander verbunden sind. In der Praxis wird oft eine Linientopologie verwendet, bei der mehrere elektronische Steuergeräte mit einer CAN-Schnittstelle passiv an einen linearen Bus angeschlossen werden. Alternativ kommt auch die passive Sterntopologie zum Einsatz.

<imgsrc="image/1705581798124.png"alt="drawing"width="600"/>

Das physische Übertragungsmedium besteht in den meisten Fällen aus einer verdrillten, ungeschirmten Zweidrahtleitung (Unshielded Twisted Pair - UTP), über die eine symmetrische Signalübertragung erfolgt. Typischerweise werden UTP-Kabel mit einem Leitungsquerschnitt zwischen 0,34 mm² und 0,6 mm² verwendet. Der Widerstandsbelag der Leitung sollte kleiner als 60 mΩ/m sein.

Die maximale Datenrate beträgt 1 MBit/s, und die zulässige Netzwerkausdehnung liegt bei etwa 40 Metern. An den Enden des CAN-Netzwerks sind Busabschlusswiderstände erforderlich, um Ausgleichsvorgänge (Reflexionen) zu vermeiden. Die ISO 11898 gibt die maximale Anzahl der CAN-Knoten mit 32 an.

### 2.2. CAN-Knoten

Mit dem fortschreitenden Trend zur Elektrifizierung von Fahrzeugen steigt die Anzahl und Komplexität der Software rapide an. Fahrzeuge der Oberklasse sind bereits mit über 1000 Software-Funktionen ausgestattet. In verschiedenen Bussystemen verrichten mehr als 70 elektronische Steuergeräte (Electronic Control Units - ECU) ihre Aufgaben. Ein elektronisches Steuergerät, das seine Funktionen in einem CAN-Netzwerk ausführt, wird als CAN-Knoten bezeichnet.

In den Anfangstagen der Vernetzung von Steuergeräten genügte ein einfacher CAN-Treiber, der eine weitgehend unkomplizierte, hardwareunabhängige Schnittstelle für die Applikation bereitstellte, sowie ein CAN-Controller und ein CAN-Transceiver für die Umsetzung der CAN-Schnittstelle. Heutzutage ist ein Betriebssystem sowie Funktionen für Netzwerkmanagement und Diagnose unverzichtbar. Die mittlerweile erhebliche Softwarekomplexität erfordert eine Standardisierung der Steuergeräteinfrastruktur.

Eine einheitliche Software verringert den Entwicklungsaufwand und erleichtert die Wartung. Sie trägt auch zur Steigerung der Wiederverwendbarkeit und Austauschbarkeit von Software-Komponenten zwischen verschiedenen Fahrzeugplattformen sowie zwischen OEMs (Original Equipment Manufacturer) und Zulieferern bei.

Mit AUTOSAR (AUTomotive Open System ARchitecture) steht eine Referenzarchitektur für die Steuergerätesoftware zur Verfügung. Im Mittelpunkt dieser Referenzarchitektur steht das AUTOSAR Runtime Environment (RTE), das das Netzwerk vollständig von den Software-Komponenten der Applikation entkoppelt. Das Runtime Environment bietet den Software-Komponenten einheitliche Dienste in Form der Basis-Software an. Diese setzt sich von unten nach oben aus drei Ebenen zusammen: Microcontroller Abstraction Layer, ECU Abstraction Layer, Service Layer.

<imgsrc="image/1705584223952.png"alt="drawing"width="600"/>

Die Abbildung "CAN-Knoten" veranschaulicht den Aufbau eines modernen CAN-Knotens. Besonders interessant ist der Bereich "Communication Services". AUTOSAR COM (Communication) stellt Standardkommunikationsdienste, Diagnosedienste (Diagnostic COM Manager) und Netzwerkmanagementdienste (Generic NM/CAN NM) bereit. Der PDU Router (PDU: Protocol Data Unit) kümmert sich um die interne Kommunikation zwischen den verschiedenen Kommunikationsschichten und koordiniert die Kommunikation zwischen AUTOSAR COM, Diagnostic COM Manager und CAN TP (Transportprotokoll).

### 2.3. CAN-Controller

Für die Teilnahme an der CAN-Kommunikation benötigt ein elektronisches Steuergerät eine CAN-Schnittstelle. Diese setzt sich aus einem CAN-Controller und einem CAN-Transceiver zusammen. Der CAN-Controller übernimmt die vorgeschriebenen Kommunikationsfunktionen des CAN-Protokolls und entlastet dabei den Host erheblich.

<imgsrc="image/1705584351782.png"alt="drawing"width="600"/>

Der CAN-Transceiver ermöglicht die Verbindung des CAN-Controllers mit dem physikalischen Übertragungsmedium. In der Regel werden beide Komponenten galvanisch durch Optokoppler getrennt, um sicherzustellen, dass Überspannungen auf dem CAN-Bus den CAN-Transceiver zwar beeinträchtigen können, jedoch nicht den CAN-Controller und den dahinterliegenden Host.

Innerhalb eines CAN-Netzwerks unterscheiden sich die CAN-Knoten hinsichtlich der Anzahl der zu sendenden und empfangenden CAN-Botschaften. Es gibt auch erhebliche Unterschiede in der Sende- und somit auch in der Empfangsfrequenz. Zum Beispiel empfängt ein CAN-Knoten fünf verschiedene CAN-Botschaften in einem Zyklus von zehn Millisekunden, während ein anderer CAN-Knoten alle 100 Millisekunden nur eine CAN-Botschaft empfängt. Diese deutlichen Unterschiede haben zwei grundlegende CAN-Controller-Architekturen hervorgebracht: solche mit und ohne Objektspeicherung.

Unabhängig vom Typ des CAN-Controllers können diese grundsätzlich integriert oder, wie in der Grafik dargestellt, als eigenständige Bausteine verwendet werden (stand-alone). In der Stand-Alone-Variante wird der CAN-Controller vom Mikrocontroller wie ein Speicherbaustein behandelt, was mehr Flexibilität bietet. Die On-Chip-Variante hingegen nimmt weniger Platz ein und ermöglicht eine schnellere und zuverlässigere Kommunikation zwischen Mikrocontroller und CAN-Controller.

### 2.4. CAN-Transceiver

Früher wurde die Verbindung des CAN-Controllers mit dem Kommunikationsmedium (CAN-Bus) oft auf diskrete Weise umgesetzt. Heutzutage übernehmen CAN-Transceiver diese Aufgabe. Da die physikalische Signalübertragung in einem CAN-Netzwerk aus elektromagnetischen Verträglichkeitsgründen symmetrisch erfolgt und das physikalische Übertragungsmedium in einem CAN-Netzwerk aus zwei Leitungen besteht, verfügt ein CAN-Transceiver stets über zwei Buspins: einen für die CAN-High-Leitung (CANH) und einen für die CAN-Low-Leitung (CANL).

<imgsrc="image/1705584603557.png"alt="drawing"width="600"/>

Üblicherweise unterscheidet man zwischen High-Speed-CAN-Transceivern und Low-Speed-CAN-Transceivern. High-Speed-CAN-Transceiver unterstützen Datenraten von bis zu 1 MBit/s, während Low-Speed-CAN-Transceiver nur Datenraten von bis zu 125 KBit/s unterstützen. Dabei gewährleisten Low-Speed-CAN-Transceiver eine fehlertolerante Auslegung der Busankopplung (zum Beispiel führt der Ausfall einer der beiden Kommunikationsleitungen nicht zum Ausfall des Kommunikationsbetriebs).

Die Abbildung „CAN-Transceiver“ zeigt den grundlegenden Aufbau eines High-Speed-CAN-Transceivers. Wenn beide Ausgangstransistoren gesperrt sind, nehmen beide CAN-Leitungen dasselbe Potenzial (0,5*Vcc) an – die Differenzspannung beträgt Null. Sobald beide Transistoren durchschalten, entsteht zwischen den Leitungen eine von der Lastwiderstand abhängige Spannungsdifferenz. Gemäß ISO 11898-2 sollte diese Differenz 2 Volt betragen. Dabei fließt ein Strom von etwa 35 mA.

<imgsrc="image/1705584619690.png"alt="drawing"width="400"/>

CAN-Transceiver sorgen im Allgemeinen für eine geringe Emission und bieten durch einen breiten Gleichtaktarbeitsbereich eine hohe Störfestigkeit. Zudem verfügen CAN-Transceiver heutzutage über einen ESD-Schutz von bis zu 8 kV. Trotz hoher Gleichtaktunterdrückung kann in besonders kritischen Anwendungsbereichen eine Gleichtaktdrossel (Common Mode Choke - CMC), die nahe am Ausgang geschaltet ist, helfen, die Emissionen weiter zu reduzieren.

Die ISO 11898 gibt die maximale Anzahl von CAN-Knoten mit 32 an. In der Praxis hängt die maximale Anzahl von CAN-Knoten jedoch stark von der Leistungsfähigkeit der eingesetzten CAN-Transceiver ab und davon, ob es sich um ein CAN-High-Speed- oder CAN-Low-Speed-Netzwerk handelt. Zum Beispiel können laut Spezifikation bis zu 110 CAN-Knoten zu einem CAN-High-Speed-Netzwerk verbunden werden, wenn der High-Speed-CAN-Transceiver TJA1050 verwendet wird.

<imgsrc="image/1705584637660.png"alt="drawing"width="400"/>

### 2.5. CAN-Bus

Die physikalische Übertragung von Signalen in einem CAN-Netzwerk basiert auf der Übermittlung von Spannungsdifferenzen, auch als Differenzialsignalübertragung bekannt. Störspannungen, die durch Motoren, Zündanlagen und Schaltkontakte erzeugt werden, können auf diese Weise effektiv neutralisiert werden. Das Übertragungsmedium, der CAN-Bus, besteht folglich aus zwei Leitungen: der CAN-High-Leitung (CANH) und der CAN-Low-Leitung (CANL).

Das Verdrillen der beiden Leitungen führt zu einer erheblichen Verringerung des magnetischen Feldes. Daher werden in der Praxis in der Regel verdrillte Leiterpaare (Twisted Pair) als physikalisches Übertragungsmedium eingesetzt.

Aufgrund der endlichen Geschwindigkeit der Signalausbreitung nimmt der Einfluss von Ausgleichsvorgängen (Reflexionen) mit steigender Datenrate oder wachsender Ausdehnung des Busses zu. Durch die Terminierung der Enden des Kommunikationskanals mit Abschlusswiderständen, die die elektrischen Eigenschaften des Übertragungsmediums nachbilden, werden Reflexionen in einem CAN-High-Speed-Netzwerk verhindert.

<imgsrc="image/1705584685403.png"alt="drawing"width="600"/>

Entscheidend für den Busabschlusswiderstand ist der sogenannte Wellenwiderstand der elektrischen Leitung, der 120 Ohm beträgt. Im Gegensatz zur ISO 11898-2, die Busabschlusswiderstände vorschreibt, sieht die ISO 11898-3 (CAN-Low-Speed) aufgrund der geringeren maximalen Datenrate von 125 KBit/s keine Busabschlusswiderstände vor.

### 2.6. CAN-Buspegel

Die physische Übertragung von Signalen in einem CAN-Netzwerk basiert auf der Übertragung von Differenzsignalen. Die Höhe der Differenzspannungen wird durch die verwendete Buskopplung bestimmt. Es gibt zwei Hauptarten von Buskopplungen: die CAN-Highspeed-Buskopplung (ISO 11898-2) und die CAN-Lowspeed-Buskopplung (ISO 11898-3).

Nach ISO 11898-2 wird der logischen 1 eine typische Differenzspannung von 0 Volt zugeordnet, während der logischen 0 eine typische Differenzspannung von 2 Volt zugewiesen wird. CAN-Highspeed-Transceiver interpretieren eine Differenzspannung von mehr als 0,9 Volt als dominanten Pegel, innerhalb des Gleichtaktarbeitsbereichs, der normalerweise zwischen 12 Volt und -12 Volt liegt.

Dagegen wird eine Differenzspannung unterhalb von 0,5 Volt als rezessiver Pegel betrachtet. Um die Immunität gegenüber Störspannungen zu erhöhen, ist eine Hysterese-Schaltung integriert. ISO 11898-3 hingegen weist der logischen 1 eine typische Differenzspannung von 5 Volt zu und der logischen 0 eine typische Differenzspannung von 2 Volt zu.

Die Grafiken "CAN-Highspeed-Buspegel" und "CAN-Lowspeed-Buspegel" veranschaulichen die verschiedenen Spannungsverhältnisse auf dem CAN-Bus.

<imgsrc="image/1705584841771.png"alt="drawing"width="400"/>

<imgsrc="image/1705584856667.png"alt="drawing"width="400"/>

### 2.7. CAN-Buslogik

Dominanter und rezessiver Buspegel im Kontext von CAN-Netzwerken spielen eine entscheidende Rolle für einen störungsfreien Kommunikationsbetrieb. Sie beeinflussen den Buszugriff, die Erkennung von Fehlern und die Bestätigung (Acknowledgement) der Übertragungen. Die Unterscheidung zwischen dominantem und rezessivem Buspegel ist dabei von essenzieller Bedeutung.

Der dominante Buspegel repräsentiert die logische „0“, während der rezessive Buspegel der logischen „1“ entspricht. Es gilt zu beachten, dass der dominante Buspegel Vorrang vor dem rezessiven hat. Wenn verschiedene CAN-Knoten gleichzeitig dominante und rezessive Buspegel senden, wird der Bus den dominanten Buspegel annehmen. Der rezessive Buspegel tritt nur dann auf, wenn alle CAN-Knoten im rezessiven Zustand senden.

Dieses Verhalten lässt sich logisch als UND-Verknüpfung interpretieren. Die physische Umsetzung erfolgt mithilfe einer sogenannten Open-Collector-Schaltung. Zur besseren Veranschaulichung und Vertiefung des Verständnisses für die zugrunde liegende Wired-AND-Buslogik in CAN-Netzwerken empfehle ich die interaktive Grafik „Buslogik“.

### 2.8. Kommunikationsprinzip

In sicherheitskritischen Anwendungsbereichen wie dem Antriebsstrang sind hohe Anforderungen an die Verfügbarkeit eines Kommunikationssystems zu erfüllen. Es wäre ungünstig, die Verantwortung für die Buszuteilung auf einen einzigen Busknoten zu übertragen, da ein Ausfall dieses exponierten Busknotens zu einem Kommunikationsausfall führen würde. Eine elegantere Lösung besteht darin, den Buszugriff zu dezentralisieren, so dass jeder Busknoten das Recht hat, auf den Bus zuzugreifen.

Ein CAN-Netzwerk basiert auf einer Kombination aus Multi-Master-Architektur und Linientopologie. In einem solchen Netzwerk ist jeder CAN-Knoten grundsätzlich berechtigt, CAN-Botschaften zu senden. Die Übertragung von CAN-Botschaften folgt keinem festgelegten zeitlichen Ablauf, sondern erfolgt ereignisorientiert. Der Kommunikationskanal wird nur dann belegt, wenn tatsächlich neue Informationen übertragen werden müssen, wodurch schnelle Buszugriffe ermöglicht werden. Dank der Fähigkeit, schnell auf asynchrone Vorgänge zu reagieren, und der hohen Datenrate von bis zu 1 MBit/s sind Echtzeitdatenübertragungen im Millisekundenbereich grundsätzlich unproblematisch.

Um Abhängigkeiten zwischen den Busknoten zu verhindern und die Konfigurationsflexibilität zu erhöhen, wird im CAN-Netzwerk eine empfängerselektive Adressierung eingesetzt. Jede CAN-Botschaft steht jedem CAN-Knoten zur Verfügung (Broadcasting), vorausgesetzt, sie ist durch eine Botschaftskennung (Identifier - ID) gekennzeichnet und wird durch eine knotenindividuelle Filterung gesteuert. Dies erhöht zwar den Aufwand, ermöglicht jedoch die Integration weiterer CAN-Knoten ohne Modifikation des CAN-Netzwerks.

Die Animation "Kommunikationsprinzip" ermöglicht es Ihnen, sich mit der Botschaftsübertragung in einem CAN-Netzwerk vertraut zu machen. Dabei lernen Sie auch den Umgang mit einer CAN-Kommunikationsmatrix und der Akzeptanzfilterung kennen. Bitte lesen Sie die Anleitung durch, um die volle Funktionalität der Animation nutzen zu können.

Die Grafik "Typische CAN-Kommunikation" setzt an die Animation "Kommunikationsprinzip" an und veranschaulicht einen typischen Ablauf der Kommunikation. Sie zeigt die zugrunde liegende Kommunikationsmatrix eines CAN-Netzwerks sowie den resultierenden Sende- und Empfangszweig.

<imgsrc="image/1705585001717.png"alt="drawing"width="800"/>

<imgsrc="image/1705585017391.png"alt="drawing"width="800"/>

<imgsrc="image/1705585034814.png"alt="drawing"width="800"/>

<imgsrc="image/1705585109881.png"alt="drawing"width="800"/>

<imgsrc="image/1705585129210.png"alt="drawing"width="800"/>

<imgsrc="image/1705585143167.png"alt="drawing"width="800"/>

<imgsrc="image/1705585155107.png"alt="drawing"width="800"/>

<imgsrc="image/1705585217149.png"alt="drawing"width="800"/>
