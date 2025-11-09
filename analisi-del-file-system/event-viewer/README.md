---
icon: calendar-days
---

# Event Viewer

L'**Event Viewer** (Visualizzatore Eventi) è uno strumento integrato in Windows che agisce come una vera e propria "scatola nera" del sistema operativo. Registra in modo cronologico ogni evento significativo: errori, avvisi, informazioni di sicurezza, avvio e arresto di servizi, e molto altro.

Per uno screenshare può risultare molto utile, poiché registra in modo affidabile proprio quelle azioni che un player potrebbe compiere per manomettere il sistema e nascondere le proprie tracce.

#### A Cosa Serve?

Mentre altri artefatti ci dicono quali file sono stati usati, l'Event Viewer ci dice **come il sistema stesso è stato usato (o abusato)**. È la nostra fonte primaria per rilevare:

* La cancellazione di altri log (come il Journal).
* La manipolazione dell'orario di sistema.
* L'arresto o il riavvio di servizi critici.

{% hint style="warning" %}
**Focus dell'Analisi**

L'Event Viewer contiene migliaia di eventi, e analizzarli tutti è impossibile e inutile. In questa guida non impareremo a leggerli tutti, ma ci concentreremo su **pochi, specifici Event ID** che sono considerati delle "smoking gun" (prove schiaccianti) per le tecniche di bypass più comuni.
{% endhint %}

#### Verifica Preliminare: Il Servizio `EventLog`

Tutto il sistema di logging dipende da un servizio fondamentale chiamato `EventLog`. Se questo servizio è disattivato, nessun evento verrà registrato. Trovarlo fermo è già di per sé un'infrazione gravissima.

*   **Come Verificare:** Apri il Prompt dei Comandi come amministratore e digita:&#x20;

    ```bash
    sc query eventlog
    ```

    **Risultato Atteso:** Lo `STATE` deve essere `RUNNING`. Se è `STOPPED`, il logging è disattivato.

Nelle pagine successive, vedremo quali ID evento cercare e come interpretarli per trovare prove concrete.
