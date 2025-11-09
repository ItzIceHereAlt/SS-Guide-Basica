---
icon: bullseye-arrow
---

# Processi Chiave da Analizzare

L'analisi della memoria non consiste nel controllare ogni singolo processo, ma nel concentrarsi su quelli che, per la loro funzione nel sistema operativo, hanno la più alta probabilità di contenere tracce di esecuzioni o attività sospette.

Di seguito sono elencati i processi "ad alto valore" da analizzare con **System Informer**.

***

#### 1. `csrss.exe` (Client Server Runtime Subsystem)

* **Funzione:** Un processo critico di Windows che gestisce finestre, thread e sottosistemi grafici.
* **Rilevanza Forense:** Per la sua natura a basso livello, la sua memoria è un registro eccellente per i percorsi di file eseguiti (`.exe`) e librerie caricate (`.dll`).
* **Come Analizzarlo:** Troverai sempre due istanze di `csrss.exe`.
  * **Per trovare file `.exe` eseguiti:**
    * Analizza l'istanza con **meno** private bytes.
    *   Usa il filtro **Regex (case-insensitive)** con il seguente pattern:

        ```
        ^[A-Z]:\\.+\.exe$
        ```
  * **Per trovare file `.dll` (injectati) o eseguibili rinominati:**
    * Analizza l'istanza con **più** private bytes.
    *   Usa il filtro **Regex (case-insensitive)** con il seguente pattern per le DLL:

        ```
        ^[A-Z]:\\.+\.dll$
        ```

{% hint style="info" %}
I percorsi trovati in `csrss.exe` sono il punto di partenza ideale per un'analisi più approfondita con **Paths Parser**, come vedremo nella prossima pagina.
{% endhint %}

***

#### 2. `PlugPlay` (servizio in `svchost.exe`)

* **Funzione:** Gestisce il riconoscimento di nuovo hardware, ma è strettamente legato all'esecuzione di applicazioni Java.
* **Rilevanza Forense:** È uno dei posti migliori per trovare tracce di esecuzione di file `.jar` (es. client o autoclicker in Java).
* **Come Analizzarlo:**
  * Individua l'istanza di `svchost.exe` che ospita il servizio `PlugPlay`.
  *   Filtra la sua memoria usando **Contains (case-insensitive)** con la stringa:

      ```
      jar
      ```

***

#### 3. `PcaSvc` (Program Compatibility Assistant Service)

* **Funzione:** Servizio che garantisce la compatibilità delle applicazioni.
* **Rilevanza Forense:** Come `PlugPlay`, la sua memoria spesso contiene tracce di esecuzione di file `.jar`, anche se avviati con metodi che potrebbero eludere altri controlli.
* **Come Analizzarlo:**
  * Individua l'istanza di `svchost.exe` che ospita il servizio `PcaSvc`.
  *   Filtra la sua memoria usando **Contains (case-insensitive)** con la stringa:

      ```
      jar
      ```
  * _Nota: Si cerca "jar" senza il punto per catturare anche eventuali argomenti da riga di comando (es. `java -jar ...`)._

***

#### 4. `dps` (Diagnostic Policy Service)

* **Funzione:** Servizio di diagnostica di sistema.
* **Rilevanza Forense:** La sua memoria è una fonte eccellente per rilevare **eseguibili con estensione rinominata (spoofed)**.
* **Come Analizzarlo:**
  * Individua l'istanza di `svchost.exe` che ospita il servizio `dps`.
  *   Usa il filtro **Regex (case-insensitive)** con il seguente pattern:

      ```
      ^!![A-Z]((?!Exe).)*$
      ```
  * Questo pattern cerca specificamente percorsi registrati dal DPS che **NON** terminano in `.exe`, un chiaro indicatore di un tentativo di occultamento.
