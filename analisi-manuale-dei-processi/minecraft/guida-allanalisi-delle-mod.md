---
icon: puzzle-piece
---

# Guida all'Analisi delle Mod

La cartella `mods` è uno dei luoghi più comuni in cui i cheater nascondono cheat, mascherandolo da mod legittima. Un'analisi metodica di questa cartella e del suo contenuto è quindi fondamentale.

**Prerequisiti:** Assicurati di aver individuato la cartella `mods` **corretta e attiva**, come spiegato nella pagina precedente, e che il tuo sistema sia configurato per visualizzare i file nascosti.

***

#### Fase 1: Controlli Preliminari sulla Cartella

Prima di analizzare i singoli file, il primo passo è ispezionare la cartella `mods` stessa.

*   **Controlla la Data di Ultima Modifica:** Esamina il timestamp "Data modifica" della cartella. Questa è una delle verifiche più rapide e importanti.



    {% hint style="danger" %}
    **Controlla la Data di Ultima Modifica**

    Esamina il timestamp "Data modifica" della cartella. Questa è una delle verifiche più rapide e importanti.

    **Indicatore Critico (Altamente Sospetto):** Se la data di modifica è molto recente (es. pochi minuti prima dell'inizio del controllo), è un **fortissimo indicatore di tampering**. Significa che i file al suo interno sono stati probabilmente aggiunti, rimossi o sostituiti nel tentativo di nascondere le prove. Molti server considerano questa una violazione direttamente sanzionabile.
    {% endhint %}

***

#### Fase 2: Analisi Dettagliata dei File `.jar`

Analizza **ogni singolo file `.jar`** presente nella cartella `mods` attiva.

**1. Identificare le Mod Caricate (Metodo Semplice)**

* Mentre il gioco è in esecuzione, prova a spostare ogni file `.jar` fuori dalla cartella `mods` (es. sul Desktop).
* I file che **non possono essere spostati** ("file in uso") sono quelli attualmente caricati dal gioco. Prendi nota di quali sono.

**2. Analisi della Dimensione (Peso)**

* Controlla la dimensione in KB o MB di ogni mod. Gli staffer esperti conoscono a grandi linee le dimensioni standard delle mod più comuni.
* **Segnale di allarme:** Una dimensione **anomala** (troppo grande o troppo piccola) rispetto alla versione ufficiale di quella mod è un forte campanello d'allarme. Ad esempio, una comune mod Togglesneak pesa circa 24-30 KB; trovarne una da 70 KB è estremamente sospetto.

**3. Analisi del Contenuto (Decompilazione con Luyten/Recaf)**

* Usa un decompilatore Java come **Luyten** o **Recaf** per ispezionare il codice delle mod sospette. Trascina semplicemente il file `.jar` nel programma.
* **Cosa cercare:**
  * **Nomi Sospetti:** Cerca classi o pacchetti con nomi che suggeriscono cheat (es. `autoclicker`, `reach`, `killaura`, `selfdestruct`).
  * **Offuscamento (Obfuscation):** Questo è un indicatore quasi certo di un cheat. L'offuscamento rende il codice illeggibile per nascondere funzionalità malevole. Si presenta con nomi di classi e metodi privi di senso, spesso con singole lettere (es. `a.class`, `b.class`) o stringhe casuali. \
    **L'offuscamento è un Red Flag.** Poiché è impossibile verificare rapidamente la sicurezza di un codice offuscato, molti server hanno una politica di **tolleranza zero** e sanzionano la presenza di mod offuscate.

**4. Verifica dell'Integrità (Controllo Hash con HashMyFiles)**

* Questo metodo è **definitivo** per provare che un file è stato manomesso.
*   **Procedura Step-by-Step:**

    1. Usa un tool come **HashMyFiles** per calcolare l'hash **SHA256** del file `.jar` del player.
    2. Trova l'hash SHA256 **ufficiale** della **stessa identica versione** della mod da una fonte attendibile (sito ufficiale dello sviluppatore, CurseForge, Modrinth).
    3. Confronta i due hash.



    {% hint style="success" %}
    **Prova Inconfutabile**

    Se gli hash non corrispondono, hai la prova definitiva che il file del player è stato modificato o che comunque non sia il file legittimo.
    {% endhint %}



***

#### Fase 3: Rilevamento di Mod "Unloaded" (Analisi della Memoria)

Questa tecnica avanzata serve a trovare mod che sono state caricate all'avvio del gioco e poi cancellate o spostate.

* **Procedura Step-by-Step:**
  1. Apri **System Informer** come amministratore.
  2. Trova il processo `javaw.exe` di Minecraft. Clic destro -> `Properties` -> `Memory` -> `Strings`.
  3. Filtra (`Contains, case-insensitive`) per il **percorso completo della cartella `mods`** del player.
  4. **Confronta** la lista di percorsi `.jar` trovati nella memoria con i file fisicamente presenti nella cartella.
* **Risultato:** Se nella memoria trovi il percorso di una mod che non è più presente nella cartella, hai la prova che è stata "unloadata" e rimossa per eludere il controllo.

***

#### Bonus: Strumenti Automatici (HabibiModAnalyzer)

Per automatizzare il controllo degli hash, puoi usare lo script PowerShell **HabibiModAnalyzer**.

* **Funzionalità:** Confronta automaticamente gli hash delle mod nella cartella con il database di Modrinth per trovare file manomessi.
*   **Comando di Esecuzione (in PowerShell come admin):**

    ```powershell
    Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass; Invoke-Expression (Invoke-RestMethod https://raw.githubusercontent.com/HadronCollision/PowershellScripts/refs/heads/main/HabibiModAnalyzer.ps1)
    ```

