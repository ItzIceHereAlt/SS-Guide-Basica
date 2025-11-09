---
icon: eraser
---

# Rilevare la Cancellazione dei Log

Cancellare i Log degli Eventi è un'azione di anti-forensics ancora più diretta della cancellazione del Journal. Significa tentare di eliminare la "memoria" stessa del sistema operativo riguardo a eventi critici come accessi, cambi di orario o manipolazione di servizi.

Fortunatamente, Windows è progettato per registrare anche questa azione di manomissione, utilizzando due ID evento distinti.

***

#### Rilevare la Cancellazione del Log di Sicurezza (ID 1102)

Questo è il controllo più importante, poiché il log di Sicurezza contiene le informazioni più sensibili.

**Procedura Step-by-Step:**

1. Apri l'**Event Viewer** (`eventvwr.msc`).
2. Nel pannello a sinistra, naviga in `Registri di Windows` > **`Sicurezza`**.
3. Nel pannello Azioni a destra, clicca su `Filtro registro corrente...`.
4. Nel campo ID evento, digita **`1102`** e clicca `OK`.

{% hint style="danger" %}
**Prova di Tampering Gravissimo 🚨**

Un evento con **ID 1102** è una delle prove più gravi di anti-forensics. Dimostra che il player ha deliberatamente tentato di nascondere attività legate alla sicurezza del sistema (come accessi o cambi di permessi).&#x20;
{% endhint %}

***

#### Rilevare la Cancellazione di Altri Log (ID 104)

Questo controllo serve a identificare la pulizia di log come "Applicazione" o "Sistema".

**Procedura Step-by-Step:**

1. Apri l'**Event Viewer** (`eventvwr.msc`).
2. Nel pannello a sinistra, naviga in `Registri di Windows` > **`Sistema`**.
3. Nel pannello Azioni a destra, clicca su `Filtro registro corrente...`.
4. Nel campo ID evento, digita **`104`** e clicca `OK`.

{% hint style="warning" %}
**Indicatore di Sospetto 🟡**

Un evento con **ID 104**, specialmente se recente, è un forte indicatore di pulizia delle tracce. I dettagli dell'evento ti diranno **quale log è stato cancellato** (es. "Il registro Applicazione è stato cancellato"). Se questo evento è vicino nel tempo ad altre attività sospette, rafforza notevolmente il caso contro il player.
{% endhint %}
