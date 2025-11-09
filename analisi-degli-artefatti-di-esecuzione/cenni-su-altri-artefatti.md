---
icon: scroll-old
---

# Cenni su Altri Artefatti

Oltre a Prefetch e BAM, che sono eccellenti per tracciare le esecuzioni più recenti, esistono altri artefatti che forniscono una preziosa **prospettiva storica** sull'attività di un sistema.

Sebbene non sempre offrano il timestamp dell'ultima esecuzione con la stessa precisione, sono fondamentali per trovare prove che sopravvivono a tentativi di pulizia e a riavvii, o per identificare software sospetto che è stato rinominato.

***

* **Amcache/Syscache**
  * **Scopo:** Un database di compatibilità che tiene traccia dei programmi eseguiti.
  * **Valore Forense:** La sua caratteristica più importante è che memorizza l'**hash SHA1** di un eseguibile. Questo permette di identificarlo con certezza (es. tramite VirusTotal) anche se il file è stato **rinominato**. Le sue voci sono molto persistenti e spesso sopravvivono alla disinstallazione del programma.
  * **Tool di Analisi:** `AmcacheParser` (Eric Zimmerman).
* **UserAssist**
  * **Scopo:** Una serie di chiavi di registro che registrano l'avvio di applicazioni tramite interfaccia grafica (GUI).
  * **Valore Forense:** Tiene traccia del **numero di esecuzioni** e dell'**orario dell'ultima esecuzione** per ogni programma, legato specificamente a un profilo utente. È utile per dimostrare un uso ripetuto di un software.
  * **Tool di Analisi:** `UserAssistView` (NirSoft) o il parser integrato in `Registry Explorer`.
* **SRUM (System Resource Usage Monitor)**
  * **Scopo:** Un database che monitora l'uso delle risorse di sistema da parte delle applicazioni.
  * **Valore Forense:** È una vera "miniera d'oro". Conserva una cronologia di **30-60 giorni** sull'esecuzione dei processi e, soprattutto, sull'**attività di rete** di ogni applicazione, inclusi i dati inviati e ricevuti.
  * **Tool di Analisi:** `SrumECmd` (Eric Zimmerman).
* **Activities Cache (Windows Timeline)**
  * **Scopo:** Alimenta la funzione "Timeline" di Windows, registrando le attività dell'utente.
  * **Valore Forense:** Fornisce una timeline ricca di contesto, mostrando non solo l'avvio di un programma, ma anche i file aperti e il tempo di utilizzo.
  * **Tool di Analisi:** `ActivitiesCache-execution` (spokwn) o `WxTCmd` (Eric Zimmerman).
* **PcaSvc (Program Compatibility Assistant)**
  * **Scopo:** Servizio che traccia l'esecuzione dei programmi per garantirne la compatibilità.
  * **Valore Forense:** Fornisce un'ulteriore prova di esecuzione che può corroborare i dati trovati in altri artefatti.
  * **Tool di Analisi:** `pcasvc-executed` (spokwn).

{% hint style="info" %}
**Perché controllare questi artefatti?**

Perché sono **persistenti**. Spesso contengono tracce di un programma anche dopo la sua disinstallazione e la pulizia di artefatti più volatili. Sono la "memoria a lungo termine" della tua indagine.
{% endhint %}
