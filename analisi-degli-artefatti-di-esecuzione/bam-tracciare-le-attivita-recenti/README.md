---
icon: chart-line-up
---

# BAM - Tracciare le Attività Recenti

Il **BAM (Background Activity Moderator)** è un servizio introdotto in Windows 10 con lo scopo di gestire le risorse delle applicazioni in background. Per svolgere questo compito, tiene traccia dei programmi eseguiti, creando uno degli artefatti forensi più affidabili e precisi per un'indagine di screenshare.

A differenza di artefatti basati su file come il Prefetch, il BAM salva le sue informazioni direttamente nel **Registro di Sistema**.

***

#### Dove si Trovano le Tracce del BAM?

Le informazioni raccolte dal BAM sono memorizzate in una chiave specifica del registro, accessibile solo con privilegi di amministratore:

{% code overflow="wrap" %}
```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\bam\State\UserSettings{User_SID}
```
{% endcode %}

All'interno di questa chiave, ogni sottocartella corrisponde a un utente del sistema, identificato dal suo **SID (Security Identifier)**. Questo garantisce che ogni traccia di esecuzione sia direttamente collegata a un account specifico.

#### Quali Informazioni Fornisce?

Per ogni programma eseguito, il BAM registra due dati fondamentali:

1. **Percorso Completo dell'Eseguibile:** Il nome stesso della voce di registro è il percorso completo del file che è stato avviato.
2. **Timestamp di Ultima Attività:** Un timestamp ad alta precisione che indica l'ultima volta che il programma è stato attivo (eseguito, chiuso o con cui si è interagito).

{% hint style="success" %}
**Perché il BAM è così potente?**

Il BAM è spesso decisivo in un controllo perché fornisce una prova di esecuzione chiara se la data di ultima attività è in istanza, con un orario preciso e direttamente attribuibile a un utente. Può contenere tracce di programmi anche se i loro file Prefetch sono stati cancellati.
{% endhint %}

Analizzare manualmente queste informazioni dal registro è complesso. Per questo motivo, si utilizzano strumenti specializzati che estraggono e decodificano questi dati in modo rapido. Nella pagina successiva, vedremo come utilizzare il tool più moderno ed efficace per questa analisi: **BAM Parser** di spokwn.
