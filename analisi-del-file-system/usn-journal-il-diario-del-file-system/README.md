---
icon: notebook
---

# USN Journal - Il Diario del File System

L'**USN Journal** è una delle risorse forensi più potenti disponibili su un sistema Windows. Pensa a esso come a un diario segreto e quasi immutabile del tuo file system: ogni singola operazione su file e cartelle viene meticolosamente annotata con un orario preciso.

Mentre altri artefatti ci dicono _se_ un programma è stato eseguito, il Journal ci racconta la **storia completa** di un file: la sua nascita, ogni sua modifica e la sua eventuale scomparsa.

***

#### Cosa Registra Esattamente?

Il Journal, memorizzato nel file di sistema nascosto `C:\$Extend\$UsnJrnl` (nel flusso `$J`), registra una vasta gamma di eventi tramite dei "codici motivo" (Reason Codes). I più importanti per un'indagine sono:

* **Creazione** di file e cartelle (`FILE_CREATE`)
* **Cancellazione** di file e cartelle (`FILE_DELETE`)
* **Rinomina** di file e cartelle (`RENAME_OLD_NAME` / `RENAME_NEW_NAME`)
* **Modifica degli attributi** (`BASIC_INFO_CHANGE`), come "Sola Lettura" o "Nascosto".
* **Modifica del contenuto** (`DATA_OVERWRITE` / `DATA_EXTEND`).

#### La Chiave per Smascherare l'Anti-Forensics

La vera forza del Journal risiede nella sua capacità di rilevare i tentativi di **occultamento delle prove**. È l'artefatto che ti permette di rispondere alla domanda: "Cosa ha cercato di nascondere il player prima del controllo?"

{% hint style="success" %}
**Il Journal trasforma l'atto di nascondere le prove in una prova stessa.**

* Un player ha cancellato i suoi file Prefetch per nascondere un'esecuzione? **Il Journal lo registra.**
* Ha rinominato un cheat per farlo sembrare un file di testo? **Il Journal lo registra.**
* Ha manipolato gli attributi di un file per "congelarne" il timestamp? **Il Journal lo registra.**
{% endhint %}

L'analisi di questo log binario richiede strumenti specializzati. Nella pagina successiva vedremo come utilizzare **JournalTrace** di spokwn per decifrare questo diario e trasformare le attività sospette in prove concrete.
