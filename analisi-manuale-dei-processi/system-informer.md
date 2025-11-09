---
icon: wrench
---

# System Informer

Se gli artefatti come Prefetch e BAM ci danno uno sguardo al passato, **System Informer** ci offre una visione in tempo reale e profonda di ciò che sta accadendo **ora** sul sistema. È un task manager avanzato, open-source e incredibilmente potente, considerato uno strumento indispensabile per qualsiasi analisi manuale.

Il suo scopo principale durante uno screenshare è permetterci di **ispezionare la memoria dei processi in esecuzione** alla ricerca di tracce che non vengono scritte su disco, come stringhe di cheat, librerie iniettate (`.dll`) o percorsi di file nascosti.

#### Configurazione Essenziale: Abilitare il Kernel-Mode Driver

Per sfruttare al massimo le capacità di System Informer e accedere anche ai processi di sistema più protetti (come `csrss.exe`), è fondamentale abilitare il suo driver a livello kernel.

**Step 1: Download e Avvio**

1. Scarica l'ultima versione di System Informer dal [**sito ufficiale**](https://systeminformer.sourceforge.io/downloads.php).
2. Avvia il programma **sempre come amministratore** (clic destro -> "Esegui come amministratore").

**Step 2: Abilitazione del Driver**

1. Dal menu in alto, vai su `Hacker` > `Options`.
2. Nella finestra delle opzioni, vai alla scheda `General`.
3. Spunta la casella **`Enable Kernel-Mode Driver`**.
4. Clicca `OK`, chiudi completamente System Informer e **riavvialo come amministratore**.

{% hint style="success" %}
Una volta completata questa configurazione, System Informer avrà i privilegi necessari per analizzare in profondità qualsiasi processo del sistema, superando molte delle restrizioni di sicurezza standard di Windows.
{% endhint %}

Nelle pagine successive vedremo quali processi analizzare e come utilizzare le potenti funzioni di ricerca di System Informer per trovare le prove.
