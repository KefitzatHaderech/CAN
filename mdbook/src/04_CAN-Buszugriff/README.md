## 4. CAN-Buszugriff

### 4.1. Prinzip des Buszugriffs

**Buszugriff für alle Knoten**

Die ISO 11898-1 definiert wegen der Sicherstellung einer hohen Verfügbarkeit und einer ereignisgesteuerten Datenübertragung eine Multi-Master-Architektur. Jeder Knoten im CAN-Netzwerk hat das Recht, ohne die Erlaubnis und ohne vorherige Absprache mit anderen CAN-Knoten zuzugreifen. Wenngleich ein Buszugriff nach ereignisgesteuertem Muster sehr rasche Reaktionen auf Ereignisse mit sich bringt, besteht prinzipiell die Gefahr, dass mehrere CAN-Knoten zum selben Zeitpunkt auf den CAN-Bus zugreifen wollen und es so zu unerwünschten Überlagerungen von Daten auf dem CAN-Bus kommt.

**Kollisionen vermeiden**

Um die Echtzeitfähigkeit des Kommunikationssystems nicht zu gefährden, sieht die ISO 11898-1 einen Buszugriff vor, der zerstörungsfreie Datenübertragung garantiert. Zum Einsatz kommt das so genannte CSMA/CA-Verfahren (Carrier Sense Multiple Access with Collision Avoidance). Das CSMA/CA-Verfahren sorgt dafür, dass sendewillige CAN-Knoten erst dann auf den CAN-Bus  zugreifen, wenn dieser frei ist.

**Bitweise Busarbitrierung**

Bei simultanen Buszugriffen sorgt die dem CSMA/CA-Verfahren zugrunde liegende Methode der bitweisen Busarbitrierung dafür, dass sich immer jener CAN-Knoten mit der höchst prioren CAN-Botschaft durchsetzt. Prinzipiell gilt: je höher die Priorität einer CAN-Botschaft, desto eher kann sie auf dem CAN-Bus übertragen werden. Niederpriore CAN-Botschaften laufen bei ungünstigem Systemdesign sogar Gefahr, gar nicht übertragen zu werden.

Zum besseren Verständnis steht Ihnen die interaktive Grafik „Prinzip des Buszugriffs“ zur Verfügung. Darin wird von zwei CAN-Knoten ausgegangen, die während einer laufenden Botschaftsübertragung auf den CAN-Bus zugreifen wollen. Bitte lesen Sie die Anleitung, um die gesamte Funktionalität des Medienobjektes zu nutzen.

**Schritt 1:**

<img src="image/README/1712022411179.png" alt="drawing" style="max-width:40%;" />

**Schritt 2:**

<img src="image/README/1712022493865.png" alt="drawing" style="max-width:40%;" />

**Schritt 3:**

<img src="image/README/1712022523730.png" alt="drawing" style="max-width:40%;" />

**Schritt 4:**

<img src="image/README/1712022543957.png" alt="drawing" style="max-width:40%;" />

### 4.2. Bitweise Arbitrierung

**Buszugriffsverfahren**

Die zentrale Komponente des von der ISO 11898-1 definierten Buszugriffsverfahrens CSMA stellt die bitweise Arbitrierung dar. Sie verhindert trotz simultanem Buszugriff das Auftreten von Kollisionen beziehungsweise löst diese auf. Das bedeutet, dass nur ein Frame die Arbitrierung unbeschadet übersteht. In der Literatur finden sich die Begriffe CSMA/CR (Collision Resolution) und CSMA/CA (Collision Avoidance). Hiermit werden die Sichtweisen des Gewinners (CSMA/CA) und der Verlierer (CSMA/CR) der Arbitrierung dargestellt.

**Eindeutige Buspegel**

Alle sendewilligen CAN-Knoten legen nach der netzwerkweiten Synchronisierung den Identifier der zu übertragenden CAN-Botschaft bitweise vom höchst- zum niederwertigsten Bit auf den CAN-Bus. Dabei sorgt die dem CAN-Netzwerkzugrunde liegende Wired-AND-Buslogik dafür, dass sich immer ein eindeutiger Buspegel einstellt.

**Arbitrierungslogik**

Die Arbitrierungslogik schließlich entscheidet, ob ein CAN-Knoten weiter senden darf, oder ob er das Senden einstellen muss. Die interaktive Grafik „Buszugriffslogik“ hilft Ihnen, die der bitweisen Arbitrierung zugrunde liegenden Mechanismen besser kennen zu lernen.

**Nur ein Knoten darf senden**

Am Ende der Arbitrierungsphase bekommt jener CAN-Knoten die Sendeberechtigung, welcher die CAN-Botschaft mit dem kleinsten ID überträgt. Unterlegene CAN-Knoten wechseln zunächst in den Empfangszustand, und greifen für einen erneuten Sendeversuch auf den CAN-Bus zu, sobald dieser wieder frei ist. Die Grafik „Buszugriffsprozedur“ ordnet alle Aktionen eines CAN-Knotens im Zusammenhang des Buszugriffs.

### 4.3.Priorisierung

Priorität und Identifier

Für den Buszugriff im CAN-Netzwerk ausschlaggebend sind die Prioritäten der CAN-Botschaften. Diese sind über den Identifier codiert und werden bitweise vom höchst- zum niederwertigsten Bit übertragen.

**Kleinerer Identifier = höhere Priorität**

Die Wired-AND-Buslogik und die Arbitrierungslogik sorgen dafür, dass mit abnehmendem Identifierwert die Priorität der CAN-Botschaft steigt: je kleiner ein Identifier ist, desto höher ist die Priorität der CAN-Botschaft. Die Grafik „Priorisierung“ verdeutlicht diesen Zusammenhang.

<img src="image/README/1712276462018.png" alt="drawing" style="max-width:40%;" />

 

**Buslast und Echtzeitfähigkeit**

Ist die Buslast nicht zu hoch, sorgt diese Art des zufälligen, zerstörungsfreien und prioritätengesteuerten Buszugriffs für einen gerechten und sehr schnellen Buszugriff. Allerdings muss berücksichtigt werden, dass mit zunehmender Buslast vor allem die Verzögerungen von niederprioren CAN-Botschaften anwachsen, was mitunter die Echtzeitfähigkeit des CAN-Kommunikationssystems beeinträchtigen kann. Beim Systemdesign sind deshalb die Prioritäten der CAN-Botschaften aus der Dringlichkeit der zu übertragenden Signale abzuleiten.

**Typische CAN-Kommunikation**

Die interaktive Grafik „Typische CAN-Kommunikation“ hilft Ihnen, den zeitlichen Kommunikationsablauf in einem CAN-Netzwerk zu verstehen. Ausgegangen wird von den in einer Kommunikationsmatrix aufgeführten Kommunikationsbeziehungen und zeitlich versetzten Ereignissen.

<img src="image/README/1712276479276.png" alt="drawing" style="max-width:40%;" />

 

**Wissensvertiefung**

Mittels der Aufgabe „Buszugriff im CAN-Netzwerk“ können Sie Ihr Wissen prüfen. Die Aufgabe bietet Ihnen die Möglichkeit, die sich aus einer zufälligen Konstellation aus Data Frames und Ereignissen resultierende Botschaftsabfolge auf dem CAN-Bus zu entwickeln.
