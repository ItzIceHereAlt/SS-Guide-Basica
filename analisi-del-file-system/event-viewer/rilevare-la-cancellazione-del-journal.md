---
icon: file-circle-xmark
---

# Rilevare la Cancellazione del Journal

La cancellazione del USN Journal è una delle tecniche di anti-forensics più drastiche. Un player la esegue per eliminare l'intera cronologia delle operazioni sui file (cancellazioni, rinomine, etc.), sperando di nascondere le proprie tracce.

Fortunatamente, questa azione lascia una firma inequivocabile nell'Event Viewer.

***

#### Procedura di Rilevamento (Step-by-Step)

**1. Apri l'Event Viewer**

* Premi `Win+R` per aprire la finestra "Esegui".
* Digita `eventvwr.msc` e premi Invio.

**2. Seleziona il Log "Applicazione"**

* Nel pannello a sinistra, naviga in `Registri di Windows` > `Applicazione`.

**3. Apri la Finestra di Filtro**

* Nel pannello "Azioni" a destra, clicca su `Filtro registro corrente...`.

**4. Inserisci l'ID Evento**

* Nella finestra di filtro, nel campo `<Tutti gli ID evento>`, digita **`3079`**.
* Clicca su `OK`.

#### Interpretazione della Prova

Se il filtro mostra uno o più eventi recenti, hai trovato la prova che stavi cercando.

{% hint style="success" %}
**Prova Inconfutabile ✅**

Un evento con **ID 3079** è la prova definitiva che il Journal di un volume è stato cancellato.

I dettagli dell'evento, come il timestamp e l'origine (spesso legata a `fsutil.exe`), forniscono tutti gli elementi necessari per sanzionare l'infrazione.
{% endhint %}
