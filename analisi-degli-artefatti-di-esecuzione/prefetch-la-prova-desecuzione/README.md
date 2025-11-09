---
icon: folder
---

# Prefetch - La Prova d'Esecuzione

Il **Prefetch** è, senza dubbio, uno degli artefatti forensi più importanti e affidabili in un'indagine di screenshare. Nato come una funzionalità di Windows per velocizzare l'avvio delle applicazioni, si è rivelato una vera e propria "scatola nera" che registra in modo preciso le esecuzioni dei programmi.

Comprendere come funziona è il primo passo fondamentale per provare l'utilizzo di un software non autorizzato.

***

#### Cos'è e Come Funziona?

Quando un'applicazione viene eseguita, il servizio di Windows chiamato **SysMain** monitora i file e i dati a cui il programma accede durante i primi secondi di avvio. Queste informazioni vengono salvate in un piccolo file con estensione `.pf` all'interno della cartella:

`C:\Windows\Prefetch`

Il nome di ogni file Prefetch segue una struttura precisa: `NOMEPROGRAMMA.EXE-HASH.pf`.

* **NOMEPROGRAMMA.EXE:** Il nome dell'eseguibile che è stato avviato.
* **HASH:** Un codice di 8 caratteri che identifica in modo univoco il **percorso** da cui il file è stato eseguito.

{% hint style="info" %}
**L'importanza dell'Hash**

L'hash non dipende dal contenuto del file, ma dal suo percorso. Questo significa che se un file `cheat.exe` viene eseguito prima dal Desktop e poi dalla cartella Download, verranno creati **due file .pf diversi**, ciascuno con un hash differente. Questo ci permette di tracciare le esecuzioni da diverse posizioni.
{% endhint %}

#### Cosa Registra il Prefetch?

Il Prefetch registra principalmente l'avvio di file eseguibili (`.exe`). Tuttavia, è cruciale per tracciare anche altri tipi di file:

* **File `.jar` (Java):** L'esecuzione di un file `.jar` non crea un file `NOMECHEAT.JAR.pf`. Invece, aggiornerà o creerà il file Prefetch per l'interprete Java, ovvero `javaw.exe.pf` o `java.exe.pf`.
* **File `.dll` (Librerie):** Le DLL non vengono eseguite direttamente. Quando vengono "iniettate", il Prefetch registra l'esecuzione del processo che le ha caricate (es. `rundll32.exe.pf`) o dell'iniettore stesso.

#### Quali Informazioni Contiene?

Ogni file `.pf` è una miniera di informazioni. Le più importanti sono:

* Il nome dell'eseguibile.
* Il numero totale di esecuzioni da quello specifico percorso.
* **L'orario esatto dell'ultima esecuzione** (questo corrisponde alla "Data Modifica" del file `.pf` stesso).
* Gli orari delle 8 esecuzioni precedenti.
* **Una lista di tutti i file e le cartelle caricati dal programma all'avvio** (noti come "Indexes" o "file referenziati").

La comprensione di questi concetti è la base per un'analisi efficace. Nelle pagine successive, esploreremo passo dopo passo come estrarre e interpretare queste informazioni utilizzando gli strumenti più adatti.
