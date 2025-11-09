---
icon: java
---

# Trovare la Cartella .minecraft Corretta

Uno degli errori più comuni e gravi in uno screenshare di Minecraft è analizzare la cartella `.minecraft` sbagliata. Molti player, specialmente quelli che usano launcher custom (Lunar, Badlion, MultiMC, etc.), non utilizzano il percorso predefinito in `%appdata%`.

Trovare la cartella **attiva**, quella che il gioco sta usando **in questo momento**, è il primo passo obbligatorio per un'indagine valida.

***

#### Metodo Convenzionale (In-Game)

Questo è il metodo più rapido e funziona nella maggior parte dei casi.

1. Con il gioco aperto, vai su `Opzioni...` > `Pacchetti di Risorse...` (`Resource Packs...`).
2. Clicca sul pulsante **`Apri la cartella dei pacchetti`** (`Open Pack Folder`).
3. Si aprirà la cartella `resourcepacks`.
4. **Sali di un livello** nella gerarchia delle cartelle (cliccando sulla cartella parente nella barra del percorso in alto).
5. **Questa è la cartella `.minecraft` corretta** che il gioco sta utilizzando in quella sessione.

***

#### Metodo Avanzato e Definitivo (Analisi della Memoria)

Questo metodo è più complesso ma è **infallibile** e necessario quando si sospettano tecniche di evasione avanzate. Il metodo convenzionale ti porta alla cartella `mods` principale, ma non garantisce che **tutte** le mod vengano caricate da lì. In teoria, è possibile caricare singole mod da percorsi differenti.

Questo metodo ti permette di trovare il percorso esatto da cui una specifica mod è stata caricata nella memoria di gioco.

**Step 1: Identifica una Mod di Riferimento**

Identifica una mod che sai per certo essere in uso in quel momento. Può essere una mod visibile a schermo (es. Keystrokes, OptiFine zoom) o una presente nella lista mod del gioco.

**Step 2: Apri System Informer**

Avvia System Informer come amministratore, con il Kernel-Mode Driver attivo.

**Step 3: Analizza il Processo `javaw.exe`**

1. Trova il processo `javaw.exe` relativo a Minecraft.
2. Clic destro -> `Properties` -> `Memory` -> `Strings`.
3. Configura la ricerca (es. `Minimum length: 5`, `Mapped` e `Private` spuntati).
4. Clicca su `Filter` e scegli `Contains (case-insensitive)`.

**Step 4: Cerca la Mod**

1. Nella barra di ricerca, digita il nome del file `.jar` della mod che hai identificato al primo passaggio (es. `OptiFine`).
2. Analizza i risultati. System Informer ti mostrerà le stringhe di memoria che contengono quel nome, incluso il **percorso completo** da cui il file è stato caricato.

{% hint style="success" %}
**Esempio di Risultato:** `C:\Users\Player\AppData\Roaming\.customlauncher\instances\1.8.9\mods\OptiFine_1.8.9_HD_U_M5.jar`

Questo percorso è la prova definitiva della cartella `mods` in uso, bypassando qualsiasi tentativo di depistaggio.
{% endhint %}

{% hint style="info" %}
**In Sintesi:** Parti sempre dal metodo convenzionale per velocità. Se hai dubbi o sospetti che il player stia usando tecniche avanzate per caricare le mod, il metodo di analisi della memoria è la tua prova del nove.
{% endhint %}
