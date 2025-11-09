---
icon: magnifying-glass
---

# Analisi delle Firme con Paths Parser (spokwn)

Dopo aver identificato i processi chiave, il passo successivo è analizzare in profondità i file che questi hanno caricato in memoria. **Paths Parser** di spokwn è lo strumento d'eccellenza per questo compito, in quanto non si limita a controllare una firma digitale, ma esegue un'analisi forense completa su ogni percorso fornito.

#### Le Funzionalità Chiave di Paths Parser

* **Verifica dell'Esistenza:** Controlla se il file esiste ancora o è stato cancellato.
* **Analisi della Firma Digitale:** Verifica la validità della firma Authenticode e rileva firme specifiche di cheat noti (es. Vape/Slinky).
* **Controlli Euristici (Generics):** Applica decine di regole per identificare caratteristiche sospette (protezioni, offuscamento, packing, funzionalità da autoclicker, etc.).
* **Rilevamento Sostituzioni (Replace):** Analizza il USN Journal per scovare tentativi di sostituzione del file.

***

#### Il Flusso di Lavoro Completo (Step-by-Step)

**Step 1: Raccogliere i Dati (i Percorsi da `csrss.exe`)**

Il tool ha bisogno di una lista di percorsi di file da analizzare. La fonte migliore è la memoria del processo `csrss.exe`.

1. Assicurati che **System Informer** sia avviato come amministratore e con il **Kernel-Mode Driver** attivo.
2. Individua il processo `csrss.exe` con **più** private bytes (ideale per trovare `.dll` e file rinominati).
3. Clic destro -> `Properties` -> `Memory` -> `Strings`.
4. Nella finestra di configurazione, imposta `Minimum length` su `5` e assicurati che `Mapped` e `Private` siano spuntati. Clicca `OK`.
5. Nella finestra dei risultati, clicca su `Filter` e scegli `Regex (case-insensitive)`.
6.  Usa il seguente pattern per estrarre tutti i percorsi di file completi:

    ```
    ^(?:\\\\\?\\)?[A-Za-z]:\\.+$
    ```
7. Una volta ottenuti i risultati, selezionali tutti (`Ctrl+A`), fai clic destro -> `Copy` -> `Copy Result`.

**Step 2: Preparare il File `paths.txt`**

1. Vai in una cartella a tua scelta (es. sul Desktop).
2. Crea un nuovo file di testo e rinominalo esattamente in **`paths.txt`**.
3. Apri il file e incolla (`Ctrl+V`) tutti i percorsi che hai copiato da System Informer. Salva e chiudi il file.

**Step 3: Eseguire l'Analisi con Paths Parser**

1. Scarica l'ultima versione di `PathsParser.exe` dal [**repository ufficiale di spokwn**](https://github.com/spokwn/PathsParser/releases).
2. Sposta il file `PathsParser.exe` **nella stessa cartella** in cui hai salvato `paths.txt`.
3. Avvia `PathsParser.exe` come amministratore. Il tool troverà e analizzerà automaticamente il file `paths.txt`.

**Step 4: Interpretare i Risultati**

Il tool mostrerà un output per ogni percorso. Ecco come leggerlo:

{% hint style="info" %}
**Decodificare l'Output di Paths Parser**

Un risultato tipico per un file sospetto potrebbe assomigliare a questo: `[DELETED] [Not Signed] [Generics: A, F2, G] C:\Users\Player\cheat.dll`

* `[DELETED] / [PRESENT]`: Indica se il file è stato cancellato o è ancora presente.
* `[Not Signed] / [Signed] / [Invalid Signature]`: Lo stato della firma. Una `.dll` non firmata (`Not Signed`) in un percorso utente è **estremamente sospetta**.
* `[Generics: ...]`: Il risultato delle euristiche. Ogni lettera indica una categoria di sospetto (es. A = Autoclicker, F = Packed/Offuscato, G = Injector). **Più "Generics" ci sono, più è probabile che sia un cheat.**
* `[REPLACE FOUND]`: Se appare questo flag, significa che il Journal mostra prove di una sostituzione del file. È una prova quasi certa di tampering.
{% endhint %}

Trovare una `.dll` non firmata, eseguita di recente (lo sai dal timestamp di altri artefatti), con un alto numero di "Generics" e magari cancellata o sostituita, costituisce una prova inattaccabile.
