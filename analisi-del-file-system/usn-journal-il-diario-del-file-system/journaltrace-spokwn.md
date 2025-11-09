---
icon: books-medical
---

# JournalTrace (spokwn)

**JournalTrace** di spokwn è lo strumento grafico (GUI) d'elezione per l'analisi del USN Journal. La sua interfaccia intuitiva e, soprattutto, il suo potente sistema di filtri, lo rendono indispensabile per trasformare un log complesso in prove chiare e leggibili.

#### Procedura di Analisi (Step-by-Step)

**Step 1: Download e Avvio**

1. Scarica l'ultima versione di `JournalTrace.exe` dal [**repository ufficiale di spokwn su GitHub**](https://github.com/spokwn/JournalTrace/releases).
2. Avvia il file **come amministratore**.

**Step 2: Scansione del Drive**

1. Una volta avviato, clicca su **`Drive`** nella barra del menu in alto.
2. Seleziona **`Select`** e scegli il drive che vuoi analizzare (solitamente `C:`).
3. Clicca nuovamente su **`Drive`** e poi su **`Scan`**. Attendi il completamento del caricamento.

**Step 3: Navigazione e Ordinamento**

1. Vai su **`Layout`** e seleziona **`Data Grid`** per visualizzare i dati in una tabella.
2. **Clicca sull'intestazione della colonna `Date`** per ordinare gli eventi dal più recente al più vecchio. Questo è il passaggio più importante per iniziare l'analisi.

#### Casi Pratici di Rilevamento con i Filtri

Ora che hai la timeline, puoi usare la barra di ricerca in alto per filtrare e trovare prove specifiche di bypass.

**Caso 1: Rilevare la Cancellazione di Artefatti (es. Prefetch)**

* **Obiettivo:** Trovare la prova che il player ha cancellato i file di Prefetch per nascondere le esecuzioni.
*   **Filtro da usare:**

    ```
    name:.pf;reason:delete
    ```
* **Cosa significa:** Questo filtro cerca contemporaneamente (`;`) nella colonna `Name` i file che contengono `.pf` e nella colonna `Reason` gli eventi di tipo `DELETE`. Trovare risultati recenti è una prova schiacciante di pulizia delle tracce.

**Caso 2: Rilevare File Ridenominati (Replace/Spoofing)**

* **Obiettivo:** Scoprire se un file è stato rinominato, una tecnica comune per nascondere un cheat (es. `vape.exe` -> `appunti.txt`).
*   **Filtro da usare:**

    ```
    reason:rename
    ```
* **Cosa significa:** Questo filtro mostra tutti gli eventi di rinomina. Vedrai due voci quasi simultanee per lo stesso file: una con `RENAME_OLD_NAME` (il nome vecchio) e una con `RENAME_NEW_NAME` (il nome nuovo), smascherando il tentativo di occultamento.

**Caso 3: Rilevare la Manipolazione di Attributi (Bypass del Read-Only)**

* **Obiettivo:** Trovare la prova che il player ha impostato un file Prefetch in "Sola Lettura" per "congelarne" il timestamp.
*   **Filtro da usare:**

    ```
    name:.pf;reason:basic_info_change
    ```
* **Cosa significa:** L'evento `BASIC_INFO_CHANGE` viene registrato ogni volta che gli attributi di un file (come "Sola Lettura") o i suoi timestamp vengono modificati. Trovare questo evento recente su un file `.pf` è un fortissimo indicatore di tampering.

{% hint style="info" %}
**Sintassi dei Filtri Avanzati**

JournalTrace supporta operatori logici per ricerche ancora più precise:

* `&&` (AND): `name:cheat&&.exe` (trova file che contengono sia "cheat" che ".exe").
* `!!` (NOT): `name:.exe!!svchost` (trova tutti gli `.exe` tranne `svchost`).
* `||` (OR): `name:.exe||.dll` (trova sia i file `.exe` che i `.dll`).
* `;` (Multi-colonna): `name:.jar;reason:delete` (cerca `.jar` nella colonna nome E `delete` nella colonna motivo).
{% endhint %}
