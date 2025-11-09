---
icon: bahai
---

# BAM Parser (spokwn)

**BAM Parser** di spokwn è lo strumento moderno di riferimento per l'analisi del Background Activity Moderator. Automatizza l'estrazione e l'analisi dei dati, arricchendoli con controlli forensi che lo rendono incredibilmente efficace.

#### Perché è lo Strumento Migliore?

* **Controllo della Sessione:** Ti dice immediatamente se un programma è stato eseguito nella sessione corrente (dall'avvio del PC).
* **Verifica della Firma Digitale:** Controlla automaticamente la firma di ogni file, segnalando quelli non firmati o con firme non valide.
* **Rilevamento Sostituzioni (Replace):** Integra un'analisi del USN Journal per scovare se un file è stato sostituito, una tecnica di bypass comune.
* **Controlli Euristici (YARA Rules):** Applica una serie di regole intelligenti per "flaggare" i file che presentano caratteristiche tipiche di cheat o malware.

#### Procedura di Analisi (Step-by-Step)

**Step 1: Download e Avvio**

1. Scarica l'ultima versione di `BAM-parser.exe` dal [**repository ufficiale di spokwn su GitHub**](https://github.com/spokwn/BAM-parser/releases).
2. Avvia il file **come amministratore**. Senza privilegi elevati, il tool non potrà accedere alle chiavi di registro necessarie.

**Step 2: Leggere l'Output - Le Colonne Chiave**

Una volta avviato, il tool analizzerà e mostrerà automaticamente le voci del BAM. Concentrati su queste colonne:

* `Last Execution User Time`: L'orario di ultima attività. Clicca qui per ordinare i risultati dal più recente.
* `In Session`: Significa che l'esecuzione è avvenuta dopo l'ultimo avvio del PC. È una prova fondamentale.
* `Signature`: Lo stato della firma digitale. Cerca `Not Signed` (non firmato) o `Invalid Signature`. Valori come `Cheat` indicano un cheat noto mentre `Fake Signature` indica una firma digitale aggiunta ma non realmente valida.
* `Journal Logs`: Se (e spesso evidenziato in rosso), il tool ha trovato prove nel Journal che il file è stato sostituito o alterato.
* `Generics`: Un punteggio basato su regole euristiche. Un numero di "Generics" superiore a 0, specialmente su un file non firmato, è un fortissimo indicatore di sospetto.

**Step 3: Filtrare per Trovare le Prove**

La lista può essere molto lunga. Usa i filtri in alto a sinistra per isolare rapidamente i file sospetti:

1. Spunta **`Only In Instance`** per vedere solo le esecuzioni della sessione corrente.
2. Spunta **`Unsigned Only`** per nascondere tutti i file legittimi e firmati digitalmente.
3. Spunta **`Flagged Only`** per mostrare solo i file che hanno attivato almeno una regola "Generic".

{% hint style="success" %}
**Come trovare un cheat in 30 secondi con BAM Parser**

1. Avvia il tool come admin.
2. Ordina per `Last Execution User Time`.
3. Spunta `Only In Instance` e `Unsigned Only`.
4. Analizza i pochi risultati rimasti: un file con un nome sospetto (es. `autoclicker.exe`) o con un alto numero di `Generics` è quasi certamente una prova.
{% endhint %}
