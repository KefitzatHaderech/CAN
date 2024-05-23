
# 3. CAN-Framing

## 3.1. Frametypen

Die ISO 11898-1 definiert den Data Frame als das Standardformat für die Übertragung von Nutzdaten im CAN-Netzwerk. Ein Data Frame kann maximal acht Nutzbytes enthalten. Dieser wird von verschiedenen Feldern umgeben, die für die Abwicklung des CAN-Kommunikationsprotokolls notwendig sind, darunter die Botschaftsadresse (Identifier - ID), der Data Length Code (DLC), die Prüfsumme (Cyclic Redundancy Check Sequence - CRC Sequence) und die Empfangsbestätigung im Acknowledgement Field.

<img src="image/README/1712276187445.png" alt="Data Frame Aufbau" style="max-width:50%;" />

Neben dem Data Frame gibt es den Remote Frame, der verwendet wird, um Nutzdaten von anderen CAN-Knoten anzufordern. Ein Remote Frame hat denselben Aufbau wie ein Data Frame, jedoch fehlt das Data Field.

<img src="image/README/1712276204782.png" alt="Remote Frame Aufbau" style="max-width:50%;" />

Der Error Frame wird verwendet, um während des Kommunikationsbetriebs entdeckte Fehler zu signalisieren. Er unterscheidet sich erheblich vom Data und Remote Frame und besteht nur aus zwei Feldern: dem Error Flag und dem Error Delimiter.

<img src="image/README/1712276232272.png" alt="Error Frame Aufbau" style="max-width:40%;" />

- **Bus Idle**: Zustand, wenn keine Botschaften übertragen werden.
- **SOF (Start of Frame)**: Anfang einer CAN-Botschaft.
- **Identifier**: Identifikationsnummer der Botschaft.
- **RTR (Remote Transmission Request)**: Unterscheidet zwischen Datenanfrage und Datenübertragung.
- **IDE (Identifier Extension)**: Unterscheidet zwischen Standard- und Extended-Format.
- **r**: Reserviertes Bit.
- **DLC (Data Length Code)**: Anzahl der Datenbytes im Data Field.
- **Data Field**: Bereich für die Nutzdaten.
- **CRC Sequence**: Prüfsumme zur Fehlererkennung.
- **DEL (Delimiter)**: Markiert das Ende der Datenübertragung.
- **ACK (Acknowledge)**: Bestätigt den Empfang einer Botschaft.
- **EOF (End of Frame)**: Markiert das Ende einer Botschaft.
- **ITM (Intermission Time)**: Pause zwischen aufeinanderfolgenden Botschaften.

## 3.2. Data Frame

Data Frames sind entscheidend für die Übertragung von Nutzdaten im CAN-Netzwerk. Sie bestehen aus mehreren Komponenten, die verschiedene Funktionen erfüllen, wie Synchronisation, Kommunikationsbeziehungen und Datensicherung.

<img src="image/README/1712276346227.png" alt="Data Frame Synchronisation" style="max-width:40%;" />

Die Übertragung eines Data Frames beginnt mit dem Startbit, auch Start Of Frame (SOF) genannt. Dieses Bit wird dominant übertragen und synchronisiert alle Knoten im Netzwerk. Der Identifier (ID) legt die Priorität des Frames fest und gewährleistet die korrekte Sender-Empfänger-Beziehung. Das RTR-Bit (Remote Transmission Request) zeigt den Frametyp an; ein dominantes RTR-Bit signalisiert einen Data Frame.

<img src="image/README/1712276365231.png" alt="Data Frame Identifier" style="max-width:40%;" />

Das IDE-Bit (Identifier Extension) unterscheidet zwischen Standard- und Extended-Format. Der DLC (Data Length Code) gibt die Anzahl der Nutzbytes an, die im Data Field übertragen werden. Maximal acht Nutzbytes sind pro Data Frame möglich.

<img src="image/README/1712276396634.png" alt="Data Frame Identifier Extension" style="max-width:50%;" />

Die Daten werden durch eine Prüfsumme (CRC) gesichert. Die Empfänger bestätigen den Empfang im ACK-Slot positiv oder negativ. Die Übertragung endet mit sieben rezessiven Bits (EOF - End Of Frame).

## 3.3. Remote Frame

Remote Frames ermöglichen die Anforderung von Nutzdaten (Data Frames) von anderen CAN-Knoten. Obwohl selten im Automobilsektor verwendet, da die Datenübertragung meist von den Informationsquellen initiiert wird, sind sie dennoch eine wichtige Funktion des CAN-Protokolls.

Der Remote Frame ähnelt dem Data Frame, abgesehen vom fehlenden Data Field. Das RTR-Bit (Remote Transmission Request) ist rezessiv, um einen Remote Frame anzuzeigen. Die Identifier von Remote und Data Frames müssen übereinstimmen, damit der empfangende Knoten entsprechend antwortet.

Bei CAN-Controllern mit Objektespeicherung erfolgt die Beantwortung eines Remote Frames automatisch. Bei Controllern ohne Objektespeicherung informiert der Controller den Host, der die Antwort initiiert.

## 3.4. Adressierung

Die Adressierung im CAN-Netzwerk basiert auf einer inhaltsbezogenen Methodik. Anstelle der Knotenadressen werden die Frames mit Identifikatoren (Identifier - ID) versehen, wodurch alle Botschaften jedem Knoten zur Verfügung stehen (Broadcasting). Die Auswahl der relevanten Botschaften erfolgt durch eine knotenindividuelle Filterung (Akzeptanzfilterung).

Der Anwender kann zwischen zwei Formaten wählen: Standard-Format (11-Bit-ID) und Extended-Format (29-Bit-ID). Im Extended-Format besteht der Identifier aus einem Basis-ID und einem Extended-ID, getrennt durch die Bits IDE und SRR. Ein dominantes IDE-Bit kennzeichnet das Standard-Format, während ein rezessives IDE-Bit das Extended-Format identifiziert.

## 3.5. CRC und Acknowledgement

Die Übertragungssicherheit im CAN-Netzwerk wird durch das CRC-Verfahren (Cyclic Redundancy Check) gewährleistet. Eine CRC-Sequenz wird basierend auf den zu übertragenden Bits berechnet und dem Datenpaket angehängt. Der Empfänger überprüft diese Sequenz, um Übertragungsfehler zu erkennen.

Empfänger bestätigen den Empfang im ACK-Slot durch ein dominantes (positive Quittung) oder rezessives Bit (negative Quittung). Ein fehlendes positives Acknowledgement führt zur Übertragung eines Error Flags und zur Unterbrechung der Nachrichtenübertragung.

## 3.6. Bitstuffing

Für eine korrekte Datenübertragung müssen die Kommunikationspartner synchronisiert sein. Die Synchronisation erfolgt durch das SOF (Start Of Frame). Der Resynchronisationsmechanismus gewährleistet, dass der Gleichlauf während der gesamten Übertragung erhalten bleibt. Der Bitstuffingmechanismus sorgt dafür, dass spätestens nach fünf homogenen Bits ein komplementäres Bit übertragen wird.

Der Bitstuffing-Bereich erstreckt sich vom SOF bis zum letzten Bit der CRC-Sequenz. Im Standard-Format können bis zu 24 Stuffbits auftreten, sodass der längstmögliche Data Frame im Standard-Format theoretisch 132 Bit umfasst.
