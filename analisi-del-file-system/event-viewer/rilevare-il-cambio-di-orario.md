---
icon: clock-rotate-left
---

# Rilevare il Cambio di Orario

La manipolazione dell'orario di sistema è una classica tecnica di anti-forensics. Viene spesso utilizzata per tentare di invalidare i timestamp di altri artefatti (**Timestomping**) e confondere la timeline di un'indagine.

Rilevare un cambio di orario **manuale** è un forte indicatore di un tentativo di bypass.

***

#### Procedura di Rilevamento (Step-by-Step)

1. **Apri l'Event Viewer** (`eventvwr.msc`).
2. Nel pannello a sinistra, naviga in `Registri di Windows` > **`Sicurezza`**.
3. Nel pannello Azioni a destra, clicca su `Filtro registro corrente...`.
4. Nel campo ID evento, digita **`4616`** e clicca `OK`.

#### Interpretazione della Prova: Automatico vs. Manuale

Trovare un evento con ID 4616 non è, da solo, una prova sufficiente. È fondamentale capire **chi o cosa** ha cambiato l'orario. Per farlo, apri i dettagli dell'evento e controlla il campo **`Nome processo`**.

* **Cambio Automatico (Legittimo):**
  * **Nome Processo:** `C:\Windows\System32\svchost.exe`
  * **Significato:** Questo è quasi sempre una sincronizzazione automatica dell'orario tramite il servizio "Ora di Windows".
* **Cambio Manuale (Altamente Sospetto):**
  * **Nome Processo:** `C:\Windows\System32\cmd.exe` o `powershell.exe`
  * **Significato:** Questo indica che l'orario è stato modificato tramite un comando manuale da riga di comando.

{% hint style="danger" %}
**Prova di Tampering 🚨**

Un cambio di orario proveniente da `cmd.exe` o `powershell.exe` è la prova quasi certa che il player ha manipolato manualmente l'orologio di sistema.
{% endhint %}
