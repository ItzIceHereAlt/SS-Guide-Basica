---
icon: folders
---

# Prefetch Parser (spokwn)

**Prefetch Parser** di spokwn è uno strumento moderno e potente che non solo analizza i file `.pf` in modo chiaro, ma integra anche controlli aggiuntivi, rendendo l'indagine più rapida e approfondita.

#### Perché Usarlo?

* **Interfaccia Intuitiva:** Presenta le informazioni in modo chiaro e organizzato.
* **Controlli Integrati:** Esegue automaticamente controlli sulla firma digitale su YARA Rules, tutto dalla stessa interfaccia.
* **Filtri Rapidi:** Permette di isolare immediatamente i file sospetti (es. non firmati o flaggati da euristiche).

#### Procedura di Analisi (Step-by-Step)

**Step 1: Avvio e Caricamento**

1. Scarica l'ultima versione di `PrefetchParser.exe` dal [**repository ufficiale di spokwn**](https://github.com/spokwn/prefetch-parser).
2. Avvia il file **come amministratore**.
3. Il tool caricherà e analizzerà automaticamente tutti i file presenti nella cartella `C:\Windows\Prefetch`.

**Step 2: Orientarsi nell'Interfaccia**

L'interfaccia è suddivisa in più sezioni:

* **Lista Principale (in alto):** Qui vedi l'elenco di tutti i file `.pf` trovati, con colonne essenziali come `Filename`, `Last Execution`, `Run Count` e `Signature`.
* **Pannello Dettagli (in basso):** Selezionando un file dalla lista, questo pannello si popola con informazioni approfondite. Le tab più importanti sono:
  * `Execution History`: Mostra gli ultimi 8 orari di esecuzione.
  * `Referenced Files`: **Fondamentale.** Mostra tutti i file e le DLL caricati dal programma all'avvio.

**Step 3: Analisi Pratica - Trovare le Prove**

Il tuo obiettivo è trovare esecuzioni recenti e sospette.

1. **Ordina per "Last Execution":** Clicca sull'intestazione della colonna `Last Execution` per ordinare i file dal più recente al più vecchio. Le attività svolte poco prima del controllo appariranno in cima.
2. **Usa i Filtri Rapidi:** In alto a sinistra, troverai dei checkbox molto utili:
   * `Show Unsigned Only`: Spunta questa casella per nascondere tutti i file con una firma digitale valida (come i processi di sistema). Questo restringe drasticamente il campo ai file potenzialmente sospetti.
   * `Flagged Only`: Mostra solo i file che sono stati "flaggati" dalle regole euristiche interne del tool, un ottimo indicatore di anomalia.
   * `Only In Instance`: Mostra solo i file eseguiti dopo l'avvio del PC, utile per concentrarsi sulla sessione corrente.
3. **Caso Pratico 1: Trovare un Cheat `.exe` Sospetto**
   * Dopo aver ordinato per data e attivato il filtro `Show Unsigned Only`, scorri la lista. Cerca eseguibili con nomi sospetti, eseguiti di recente, da percorsi anomali (es. `Downloads`, `Desktop`, cartelle temporanee). La colonna `Signature` che riporta `Not Signed` o `Invalid Signature` è un forte campanello d'allarme.
4. **Caso Pratico 2: Trovare un Cheat `.jar` (es. Autoclicker)**
   * Nella barra di ricerca, digita `javaw.exe`.
   * Seleziona l'entry `JAVAW.EXE-XXXXXXXX.pf` più recente.
   * Nel pannello in basso, vai alla tab `Referenced Files`.
   * Nella barra di ricerca di questo pannello, digita `.jar`.
   * Il risultato ti mostrerà il percorso completo del file `.jar` che è stato eseguito, come ad esempio `C:\Users\Player\Downloads\autoclicker.jar`.

{% hint style="success" %}
Questo metodo è estremamente efficace per collegare un processo generico come `javaw.exe` a un file specifico, fornendo una prova inconfutabile. Lo stesso principio si applica per trovare le `.dll` caricate da processi come `rundll32.exe`.
{% endhint %}
