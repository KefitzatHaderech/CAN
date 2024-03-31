
## 5. CAN-Datensicherung

### 5.1. Prinzip der Datensicherung

Datenintegrität im Kfz

Eine sichere Datenübertragung ist die Voraussetzung für die Sicherheit elektronischer Systeme im Kfz. CAN hat folglich nicht nur strengen Anforderungen an die Echtzeit zu genügen, sondern in jedem Fall auch für eine sichere Datenübertragung zu sorgen. Weil CAN innerhalb des Kfz auch in sehr zeit- und sicherheitskritischen Anwendungen zum Einsatz kommt, sind die Anforderungen an die Datenintegrität äußerst hoch.

Elektromagnetische Verträglichkeit (EMV)

Zur Bewertung der Datenintegrität von Bedeutung sind grundsätzlich die Umgebung, die störend auf die Datenübertragung einwirkt und die Fähigkeit des seriellen Bussystems, Störungen abzuwehren. Die Gewährleistung einer sicheren Datenübertragung beginnt deshalb bereits mit der physikalischen Systemauslegung, wobei die elektromagnetische Verträglichkeit (EMV) traditionell einen großen Raum einnimmt.

Mögliche Fehlerquellen

Trotz elektromagnetisch verträglichem Design und physikalischer Datensicherung kann es zu galvanischen, induktiven und kapazitiven Kopplungen, zu Signaldämpfungen und Signalverzerrungen kommen. Man denke auch an unterschiedliche Abtastzeitpunkte, unterschiedliche Schaltschwellen und Frequenzabweichungen zwischen den Kommunikationspartnern - von einer störungsfreien Datenübertragung kann nicht ausgegangen werden.

Minimierung der Restfehler-wahrscheinlichkeit

Die Datenintegrität lässt sich als Produkt aus der Wahrscheinlichkeit, mit der die Daten während der Übertragung gestört und verfälscht werden, und der Wahrscheinlichkeit, dass gestörte Daten unerkannt bleiben, auffassen. Prinzipiell ergeben sich somit zwei Strategien zur Minimierung der Restfehlerwahrscheinlichkeit bzw. zur Erhöhung der Datenintegrität.

Da wäre einerseits die Vermeidung von verfälschten Daten mittels elektromagnetisch verträglicher Netzwerkauslegung bzw. physikalischen Maßnahmen (u.a. Twisted Pair), andererseits die Erkennung und Korrektur von verfälschten Daten mittels leistungsfähiger logischer Fehlererkennung und einer effektiven logischen Fehlerbehandlung. Die Grafik „Prinzip der Datensicherung im CAN-Netzwerk" gibt dazu einen Überblick.

![1706366486155](image/1706366486155.png)

### 5.2. NRZ-Codierung

Bitcodierung

Sich mit der Vermeidung von Störungen zu beschäftigen heißt, sich mit Emissionen und Immissionen bzw. Störfestigkeit auseinanderzusetzen. Von großer Bedeutung für die Abstrahlleistung ist die Bitcodierung. Eine kluge Bitcodierung hilft, die Emissionen wesentlich zu reduzieren. Allerdings hat man diese Forderung häufig mit einer geforderten Transportkapazität in Einklang zu bringen.

NRZ-Bitcodierung

Für CAN wurde die NRZ-Bitcodierung (Non Return to Zero) gewählt. Das heißt, die zu übertragenden Binärsignale werden direkt abgebildet: eine logische „1“ durch einen hohen Pegel, eine logische „0“ durch ein niedrigen Pegel. Charakteristisch für die NRZ-Codierung ist es, dass bei aufeinander folgenden Bits gleicher Polarität keine Pegeländerung stattfindet.

Fehlende Synchronisation

Die NRZ-Codierung erlaubt so höchste Datenraten und hält die Emission in Grenzen. Jedoch ist die NRZ-Codierung nicht selbsttaktend, besitzt also keine Synchronisiereigenschaften: wenn über längere Zeit keine Pegeländerung stattfindet, dann verliert der Empfänger die Synchronisation. Deswegen erfordert der Einsatz der NRZ-Codierung einen expliziten Synchronisationsmechanismus, der allerdings die Übertragungseffizienz verringert.

Bitstuffing zur Synchronisation

Bei CAN kommt als Synchronisationsmechanismus das sog. Bitstuffingverfahren zum Einsatz: nach fünf homogenen Bits fügt der Sender ein komplementäres Bit in den Bitstrom ein (die Manchester-Codierung beispielsweise kommt ohne einen solchen Mechanismus aus, da sie selbsttaktend ist).

![1706366510245](image/1706366510245.png)

### 5.3. Twisted Pair

Symmetrische Signalübertragung

Die beispielsweise durch Motoren, Zündanlagen und Schaltkontakte induzierten Störspannungen können effektiv durch die symmetrische Signalübertragung unschädlich gemacht werden. Bei der symmetrischen Signalübertragung wirkt sich eine äußere Störung auf beide Leitungen gleichermaßen aus.

Differenzbildung

Durch die Differenzbildung hebt sich also das Störsignal auf - das Nutzsignal wird deshalb nicht beeinflusst. Aus der symmetrischen Signalübertragung resultiert ein physikalisches Übertragungsmedium CAN-Bus, welches sich aus zwei Leitungen zusammensetzt:
CAN-High-Leitung (CANH) und CAN-Low-Leitung (CANL).

Magnetische Felder

Im Hinblick auf Abstrahlung von Systemen mit symmetrischer Signalübertragung nutzen wir den Vorteil der die Drähte umgebenden magnetischen Felder. In den Drähten sind die elektrischen Felder exakt entgegengesetzt und somit auch die resultierenden magnetischen Felder um die Drähte herum. Verlegt man nun die beiden Drähte eng aneinandergeschmiegt, so heben sich die magnetischen Felder und damit die Abstrahlung fast gänzlich auf. Das enge aneinander Liegen der CAN-Drähte garantiert man durch ihr Verdrillen. Man spricht von verdrillten Leitungspaaren, sogenannten Twisted Pairs.

Mehr Umschlingungen = weniger Einflüsse

Durch das Verdrillen wird die Leiterschleife in einzelne Leiterstücke zerlegt. Im Idealfall zeigen die Magnetfelder in jedem Teilstück in entgegengesetzte Richtungen, was dazu führt, dass sich die induzierten Spannungen bzw. die induktiven Einflüsse gegenseitig aufheben. Die Wirksamkeit der Verdrillung steigt mit der Anzahl der Umschlingungen. Mindestens 30 Umschlingungen pro Meter sorgen für gute Ergebnisse.

![1706366533286](image/1706366533286.png)

### 5.4. Terminierung

Wellenwiderstand

Mit steigender Datenrate muss auf dem CAN-Bus aufgrund der endlichen Signalausbreitung mit Ausgleichsvorgängen in Form von Reflexionen gerechnet werden. Dies ist der Grund, warum in CAN-High-Speed-Netzwerken die Bus-Enden mit dem Wellenwiderstand des physikalischen Übertragungsmediums abgeschlossen werden müssen. Der Wellenwiderstand des Kommunikationskanals beträgt 120 Ohm.[]

![1706366559944](image/1706366559944.png)

Abschluss­widerstand

Anstatt die Enden des Kommunikationskanals mit jeweils einem einzelnen Busabschlusswiderstand zu versehen, können die Enden des CAN-Busses auch mit einem geteiltem Busabschluss terminiert werden. Der geteilte Busabschluss, bestehend aus zwei identischen Widerständen (60 Ohm) und einer Kapazität (typischerweise 4,7 nF), wirkt wie ein Tiefpassfilter: ohne Beeinflussung der Gleichspannungsverhältnisse werden hochfrequente Signale gegen Masse kurzgeschlossen. Messungen haben gezeigt, dass sowohl die Störfestigkeit verbessert als auch die Emissionen reduziert werden können.

![1706366572774](image/1706366572774.png)

### 5.5. Logische Fehlererkennung

Fünf Fehlererkennungs­mechanismen

Zur Erkennung verfälschter Botschaften definiert das CAN-Protokoll fünf Maßnahmen: Bitmonitoring, Überwachung des Botschaftsformats (Form-Check), Überwachung der Bitcodierung (Stuff-Check), Auswertung des Acknowledgements (ACK-Check) und Auswertung der Prüfsumme (Cyclic Redundancy Check).

Aufgaben für Sender und Empfänger

Die Fehlererkennungsmechanismen Bitmonitoring und ACK Check werden vom Sender einer CAN-Botschaft wahrgenommen. Unabhängig von der Akzeptanzfilterung kümmern sich die Empfänger um Form Check, Stuff Check und Cyclic Redundancy Check. Die Grafik „Fehlererkennung“ zeigt Ihnen, welche Felder eines Data oder Remote Frames von den einzelnen Fehlererkennungsmechanismen betroffen sind.

Stuff Check,

Empfänger

Der Stuff Check dient der Überprüfung des Bitstroms. Das CAN-Protokoll schreibt dem Sender aus Gründen der Synchronisation vor, nach fünf homogenen Bits ein komplementäres Bit zu übertragen. Ein Stuffingfehler liegt dann vor, wenn ein Empfänger nach fünf homogenen Bits ein weiteres Bit derselben Polarität entdeckt.

Bitmonitoring,

Sender

Im Rahmen des Bitmonitorings vergleicht der Sender jeden gesendeten Bitpegel mit dem tatsächlichen Buspegel. Ein Bitfehler liegt vor, wenn der Sender eine Diskrepanz zwischen beiden Pegeln entdeckt. Das Bitmonitoring sorgt dafür, dass alle globalen Fehler und alle lokal beim Sender auftretenden Fehler entdeckt werden.

Form Check,

Empfänger

Der Form Check dient der Überprüfung des Formats einer CAN-Botschaft. Jede CAN-Botschaft weist an bestimmten Stellen immer dieselben Bitsequenzen auf. Dabei handelt es sich um den CRC-Delimiter, den ACK-Delimiter und um das EOF. Diese Botschaftskomponenten werden vom Sender stets rezessiv übertragen. Ein Formatfehler liegt dann vor, wenn ein Empfänger mittels Form-Check einen dominanten Buspegel innerhalb einer dieser Botschaftskomponenten entdeckt.

Cyclic Redundancy Check (CRC),

Empfänger

Beim Cyclic Redundancy Check (CRC) geht man davon aus, dass das dem ankommenden Data oder [Remote Frame](https://elearning.vector.com/mod/page/view.php?id=48 "Remote Frame") entsprechende Polynom R(x) einem Vielfachen des durch die ISO 11898-1 spezifizierten Generatorpolynoms G(x) entspricht. Wenn dies nicht der Fall ist (CRC-Fehler), dann wurde das Data oder [Remote Frame](https://elearning.vector.com/mod/page/view.php?id=48 "Remote Frame") während der Übertragung vom Sender zum Empfänger verfälscht.

ACK Check,

Sender

Der im CAN-Protokoll definierte Bestätigungsmechanismus (Acknowledgement) sieht vor, dass alle Empfänger jede ankommende CAN-Botschaft im Anschluss an den Cyclic Redundancy Check bestätigen müssen. Eine einzige positive Bestätigung reicht aus, um dem Sender zu signalisieren, dass mindestens ein Empfänger die von ihm übertragende CAN-Botschaft korrekt empfangen hat. Wenn keine einzige positive Bestätigung beim Sender eintrifft, dann liegt ein Bestätigungsfehler (ACK-Fehler) vor.

![1706366600882](image/1706366600882.png)

![1706366613193](image/1706366613193.png)

![1706366622170](image/1706366622170.png)

![1706366631728](image/1706366631728.png)

![1706366639960](image/1706366639960.png)

![1706366649284](image/1706366649284.png)

### 5.6. Logische Fehlerbehandlung

Netzwerkweite Datenkonsistenz

Das CAN-Protokoll schreibt aus Gründen netzwerkweiter Datenkonsistenz vor, dass bei lokalen Störungen der fehlererkennende [CAN-Knoten](https://elearning.vector.com/mod/page/view.php?id=39 "CAN-Knoten") alle im [CAN-Netzwerk](https://elearning.vector.com/mod/page/view.php?id=38 "CAN-Netzwerk") angeschlossenen [CAN-Knoten](https://elearning.vector.com/mod/page/view.php?id=39 "CAN-Knoten") davon in Kenntnis zu setzen hat. Dazu überträgt der fehlererkennende [CAN-Knoten](https://elearning.vector.com/mod/page/view.php?id=39 "CAN-Knoten") ein Fehlersignal (Error Flag), welches sich aus sechs dominanten Bits zusammensetzt. Damit wird bewusst die Bitstuffingregel verletzt und so ein [Bitstuffing](https://elearning.vector.com/mod/page/view.php?id=51 "Bitstuffing")-Fehler verursacht.

Error Flags

Die Übertragung eines Error Flags sorgt also dafür, dass alle anderen [CAN-Knoten](https://elearning.vector.com/mod/page/view.php?id=39 "CAN-Knoten") ebenfalls einen Error Flag (sekundäres Error Flag) übertragen und somit ebenfalls wie der Sender des primären Error Flags die reguläre Datenübertragung abbrechen. Je nach Situation können sich primäres und sekundäres Error Flag auch überlagern.

Error Delimiter

Der Übertragung eines Error Flags schließt sich immer die Übertragung eines Error Delimiters an. Dieser setzt sich aus acht rezessiven Bit zusammen. Der Error Delimiter ersetzt den ACK-Delimiter und das EOF einer regulären Botschaftsübertragung, so dass sich zusammen mit der obligatorischen Sendepause (ITM - Intermission) auf dem [CAN-Bus](https://elearning.vector.com/mod/page/view.php?id=43 "CAN-Bus") elf rezessive Bit ergeben (Bus-Idle-Kennung). []

Abschluss der Fehlerbehandlung

Die Fehlerbehandlung wird vom Sender der abgebrochenen CAN-Botschaft abgeschlossen, indem er nach dem ITM versucht, die abgebrochene CAN-Botschaft nochmals zu übertragen. Die Grafik „Fehlerbehandlung“ fasst alle Aktionen, die nach der Fehlererkennung in einem [CAN-Netzwerk](https://elearning.vector.com/mod/page/view.php?id=38 "CAN-Netzwerk") ablaufen, zusammen. Die Animation „Bitmonitoringfehler“ lädt Sie ein, sich mit der Fehlerbehandlung am Beispiel eines Bitmonitoringfehlers interaktiv auseinanderzusetzen.

Keine Garantie für sofortige Wiederholung

Aufgrund des prioritätengesteuerten Buszugriffs gibt es keine Garantie für die sofortige Wiederholung. Im besten Fall dauert es von der Fehlerentdeckung bis zum Wiederaufsetzen 17 Bitzeiten (primäres Error Flag, Error Delimiter, ITM). Es dauert 23 Bitzeiten, wenn sich primäres und sekundäres Error Flag nicht überlagern.

Suspend Transmission Time

31 Bitzeiten dauert es, wenn sich der [CAN-Knoten](https://elearning.vector.com/mod/page/view.php?id=39 "CAN-Knoten") im fehlerpassiven Zustand befindet. In diesem Zustand hat ein [CAN-Knoten](https://elearning.vector.com/mod/page/view.php?id=39 "CAN-Knoten") die sog. Suspend Transmission Time abzuwarten, ehe er wieder auf den [CAN-Bus](https://elearning.vector.com/mod/page/view.php?id=43 "CAN-Bus") zugreifen darf. Bei der Suspend Transmission Time handelt es sich also um eine verordnete Sendepause von 8 Bits.

![1706366676774](image/1706366676774.png)

![1706366686255](image/1706366686255.png)

### 5.7. Fehlerverfolgung

Busblockade vermeiden

Zur Sicherstellung netzweiter Datenkonsistenz besitzt jeder Knoten in einem [CAN-Netzwerk](https://elearning.vector.com/mod/page/view.php?id=38 "CAN-Netzwerk") das Recht, eine als fehlerhaft interpretierte CAN-Botschaft abzubrechen. Dies gilt auch für [CAN-Knoten](https://elearning.vector.com/mod/page/view.php?id=39 "CAN-Knoten"), die irrtümlicherweise korrekte CAN-Botschaften als fehlerhaft interpretieren. Um die Blockierung des Übertragungsmediums zu vermeiden, hat man im CAN-Protokoll eine Fehlerverfolgung definiert, mit der die [CAN-Knoten](https://elearning.vector.com/mod/page/view.php?id=39 "CAN-Knoten") gelegentlich auftretende von anhaltenden Störungen unterscheiden können.

TEC und REC

Im Zuge dessen führt jeder [CAN-Controller](https://elearning.vector.com/mod/page/view.php?id=40 "CAN-Controller") einen Sendefehlerzähler TEC (Transmit Error Counter) und einen Empfangsfehlerzähler REC (Receive Error Counter). Im Falle einer erfolgreichen Übertragung eines Data oder Remote Frames wird der entsprechende Fehlerzähler dekrementiert (TEC=TEC-1; REC=REC-1). Durch das Entdecken und anschließende Übertragen eines Error Flags wird der entsprechende Fehlerzähler nach bestimmten Regeln inkrementiert. Für den Sender gilt folgende Regel: TEC=TEC+8. Fehlererkennende Empfänger inkrementieren ihren REC zunächst um eine Einheit (REC=REC+1). Für den Fehler verursachenden Empfänger gilt zudem REC=REC+8.

Error Active

In Abhängigkeit des jeweiligen Zählerstands unternimmt ein [CAN-Controller](https://elearning.vector.com/mod/page/view.php?id=40 "CAN-Controller") die Umschaltung des Fehlerzustandes. Nach dem Start nimmt ein [CAN-Controller](https://elearning.vector.com/mod/page/view.php?id=40 "CAN-Controller") den Normalzustand Error Active ein. In diesem Zustand überträgt der [CAN-Controller](https://elearning.vector.com/mod/page/view.php?id=40 "CAN-Controller") nach Detektion eines Fehlers sechs dominante Bit (aktives Error Flag). Nach Überschreiten einer Grenze (TEC>127; REC>127) wechseln die [CAN-Controller](https://elearning.vector.com/mod/page/view.php?id=40 "CAN-Controller") in den Zustand Error Passive.

Error Passive

[CAN-Controller](https://elearning.vector.com/mod/page/view.php?id=40 "CAN-Controller") im Zustand Error Passive können einen entdeckten Fehler lediglich mit sechs homogenen rezessiven Bits signalisieren. Fehlererkennenden Empfängern wird so die Möglichkeit genommen, entdeckte Fehler zu globalisieren. [CAN-Controller](https://elearning.vector.com/mod/page/view.php?id=40 "CAN-Controller"), die sich im Zustand Error Passive befinden, müssen beim Senden von zwei aufeinanderfolgenden Data oder Remote Frames zusätzlich die „Suspend Transmission Time“ (8 Bits) abwarten.

Bus Off

Bei Ausfall eines CAN-Controllers oder bei extremer Fehlerhäufung erfolgt ein Zustandsübergang nach Bus Off. Der [CAN-Controller](https://elearning.vector.com/mod/page/view.php?id=40 "CAN-Controller") trennt sich vom [CAN-Bus](https://elearning.vector.com/mod/page/view.php?id=43 "CAN-Bus") ab. Der Zustand Bus Off kann nur durch Eingriff des Host (mit 128 x 11 Bit Zwangswartezeit) oder per Hardware-Reset verlassen werden.

![1706366752481](image/1706366752481.png)
