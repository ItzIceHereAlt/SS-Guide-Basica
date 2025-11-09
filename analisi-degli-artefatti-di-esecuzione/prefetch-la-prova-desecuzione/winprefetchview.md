---
icon: magnifying-glass
---

# WinPrefetchView

**WinPrefetchView** di NirSoft è uno degli strumenti più classici e diretti per l'analisi dei file Prefetch. La sua interfaccia semplice lo rende un ottimo punto di partenza per chiunque si avvicini a questo tipo di indagine.

#### Perché Usarlo?

* **Semplicità:** È estremamente facile da usare. Basta avviarlo per avere subito una panoramica completa.
* **Affidabilità:** Essendo uno strumento consolidato, è molto affidabile nell'estrarre le informazioni di base dai file `.pf`.
* **Leggerezza:** Non richiede installazione ed è un programma molto leggero.

#### Procedura di Analisi (Step-by-Step)

**Step 1: Avvio e Configurazione Iniziale**

1. Scarica WinPrefetchView dal **sito ufficiale di NirSoft** (cerca "WinPrefetchView").
2. Avvia il file `WinPrefetchView.exe` **come amministratore**. Il programma caricherà automaticamente i file dalla cartella di Prefetch.

**Step 2: Ordinare le Prove**

L'interfaccia principale è una singola tabella. La prima e più importante azione da compiere è ordinare i dati per trovare le attività più recenti.

1. Clicca sull'intestazione della colonna **"Modified Time"**. Clicca una seconda volta se necessario per assicurarti che le date più recenti siano in cima (ordine decrescente).
2. Questo ti mostrerà immediatamente quali programmi sono stati eseguiti per ultimi.

**Step 3: Analisi Pratica - Trovare le Prove**

Ora che hai la timeline, puoi iniziare a cercare le evidenze.

* **Lista Principale (Pannello Superiore):**
  * Scorri la lista alla ricerca di nomi di file sospetti (`.exe`) eseguiti di recente. Presta particolare attenzione a file situati in percorsi insoliti come `Downloads`, `Desktop` o cartelle con nomi casuali.
  * Cerca la presenza di file `.pf` con estensioni anomale, come `NOMEFILE.TMP-HASH.pf`. Questo è un forte indicatore di un eseguibile rinominato (spoofed extension).
* **Dettagli dei File Referenziati (Pannello Inferiore):**
  * Questa è la funzionalità più potente di WinPrefetchView per un'indagine. Selezionando una riga nel pannello superiore, il pannello inferiore si popola con la lista di tutti i file e le cartelle caricati da quel programma.

**Caso Pratico: Trovare un Cheat `.jar` o una `.dll`**

1. **Trova il Processo "Ospite":** Nel pannello superiore, cerca e seleziona il file `.pf` del processo che ha eseguito il cheat.
   * Per un cheat `.jar`, cerca `javaw.exe.pf` (o `java.exe.pf`).
   * Per una cheat `.dll` iniettata, cerca `rundll32.exe.pf`, `regsvr32.exe.pf` o il `.pf` dell'iniettore, se noto.
2. **Filtra i File Caricati:** Con il processo "ospite" selezionato, sposta l'attenzione sul pannello inferiore.
3. Usa la funzione di ricerca (`Ctrl+F`) in questo pannello e cerca l'estensione che ti interessa (es. `.jar` o `.dll`).
4. Il risultato mostrerà il percorso completo del file che è stato caricato, fornendo la prova che collega l'esecuzione generica di `javaw.exe` a un file specifico come `C:\Users\Player\Downloads\autoclicker.jar`.
