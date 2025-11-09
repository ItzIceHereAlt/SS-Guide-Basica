---
icon: brain-circuit
---

# Analisi della Memoria Kernel con Kernel Live Dump Analyzer (spokwn)

Alcune delle tecniche di bypass più avanzate, come le esecuzioni "fileless" o i comandi di pulizia eseguiti da riga di comando (`cmd`, `powershell`), non lasciano tracce evidenti negli artefatti standard. Tuttavia, la **memoria del kernel** di Windows spesso conserva frammenti di questi comandi anche dopo la chiusura del terminale.

L'analisi di un **Kernel Live Dump** è una tecnica potente per scovare queste prove nascoste. Il **Kernel Live Dump Analyzer** di spokwn automatizza questo processo, scansionando il dump di memoria alla ricerca di stringhe e comandi sospetti.

***

#### Procedura di Analisi (Step-by-Step)

**Step 1: Creare il Kernel Live Dump**

Il tool ha bisogno di un file `.dmp` su cui lavorare. Il modo migliore per crearlo è tramite **System Informer**.

1. Assicurati che System Informer sia in esecuzione come **amministratore** e con il **Kernel-Mode Driver** attivo.
2. Cerca il processo `System`  > `Create kernel memory dump`.
3. Seleziona **`Live kernel dump Full`**.
4. Attendi il completamento del processo. System Informer salverà un file `.dmp` sul sistema. Prendi nota del percorso in cui viene salvato.

**Step 2: Preparare l'Ambiente di Analisi**

1. Scarica `Kernel-Live-Dump-Analyzer.exe` dal [**repository ufficiale di spokwn**](https://github.com/spokwn/Kernel-Live-Dump-Analyzer/releases).
2. Sposta o copia il file `.dmp` creato al passaggio precedente.
3. **Cruciale:** Posiziona `Kernel-Live-Dump-Analyzer.exe` **nella stessa identica cartella** del file `.dmp`.

**Step 3: Eseguire l'Analisi**

1. Avvia `Kernel-Live-Dump-Analyzer.exe` (consigliato come amministratore).
2. Il tool rileverà automaticamente il file `.dmp` nella sua cartella e inizierà l'analisi. Il processo è molto rapido.

**Step 4: Analizzare l'Output**

Al termine, il tool creerà una nuova cartella chiamata `results`. All'interno troverai uno o più file `.txt` contenenti le stringhe sospette trovate nel dump della memoria.

Apri i file di testo e cercali (`Ctrl+F`).

{% hint style="info" %}
**Cosa Cercare nei Risultati?**

Cerca comandi che indicano un tentativo di bypass o di pulizia delle tracce, come:

* Comandi di cancellazione: `reg delete`, `fsutil usn deletejournal`, `wevtutil cl`.
* Esecuzioni nascoste: `wmic process call create`, `powershell -e` (indica un comando codificato), `IEX (New-Object Net.WebClient)`.
* Manipolazione di file: `type file1.exe >> file2.txt:stream` (indica un ADS), `icacls C:\Windows\Prefetch /deny...`.
* Percorsi di file sospetti o nomi di cheat.
{% endhint %}

{% hint style="warning" %}
**Attenzione:** Questa è una tecnica avanzata. La creazione di un dump della memoria può essere un'operazione intensiva. Utilizzala quando hai un forte sospetto di bypass da riga di comando o fileless e le altre analisi non hanno dato risultati.
{% endhint %}
