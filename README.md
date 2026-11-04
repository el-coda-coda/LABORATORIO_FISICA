# LABORATORIO DI FISICA

Repository condiviso per il materiale di laboratorio A.A. 2026-2027. La libreria a cui fanno riferimento i codici è la mia libreria python che è pubblicata [qui](https://pypi.org/project/lab-physics-tools/). Mentre per il codice e possibili applicazioni/esempi c'è il [repository](https://github.com/el-coda-coda/LabPhysicsTools.git). 

---

## 1. Regole per il lavoro condiviso

1. Evitare modifiche concorrenti su file non testuali: file come .ods (LibreOffice) e .lyx sono binari/compressi. Git non puo fare il merge automatico riga per riga; se due persone toccano lo stesso file insieme, si crea un conflitto non gestibile.
2. Aggiornare sempre prima di modificare: eseguire sempre il download delle ultime modifiche da remoto prima di iniziare a lavorare in locale.
3. Commit piccoli e mirati: registrare le modifiche quando si completano blocchi logici precisi (es. "Aggiunta simulazione filtro passa-basso"), evitando commit generici come "test" o "update".
4. Nessun file generato o temporaneo: non tracciare file .raw, .log, .op.raw o file di swap/backup (*~).

---

## 2. Setup iniziale (solo al primo clone)

Clonare il repository e impostare il rebase automatico per le operazioni di sincronizzazione:

    git clone https://github.com/el-coda-coda/LABORATORIO_FISICA.git
    cd LABORATORIO_FISICA
    git config pull.rebase true

---

## 3. Workflow standard su branch principale (main)

Flusso da seguire per modifiche ordinarie e sincronizzate:

    # 1. Scarica sempre l'ultima versione prima di iniziare
    git pull

    # 2. Modifica i file in locale e controlla lo stato
    git status

    # 3. Metti in staging i file modificati
    git add nome_del_file
    # oppure per aggiungere tutte le modifiche:
    git add .

    # 4. Registra il commit con un messaggio descrittivo
    git commit -m "Descrizione precisa della modifica"

    # 5. Invia le modifiche a GitHub
    git push origin main

---

## 4. Gestione Branch e Pull Request

Consigliato per sviluppare nuove sezioni della relazione o script di analisi senza rischiare di bloccare gli altri componenti del gruppo.

Creazione e lavoro su un nuovo branch:

    # Crea un nuovo branch e spostati su di esso
    git switch -c feature-analisi-dati

    # Lavora normalmente, poi salva le modifiche
    git add .
    git commit -m "Completata analisi dati e fit lineare"

    # Invia il branch su GitHub (solo la prima volta richiede -u)
    git push -u origin feature-analisi-dati

Unione del branch (Merge):

Metodo 1: Tramite interfaccia web GitHub (Consigliato)
1. Aprire la pagina del repository su GitHub.
2. Cliccare sul pulsante "Compare & pull request" comparso in alto.
3. Inserire una breve descrizione e confermare con "Create pull request".
4. Revisionato il codice, cliccare su "Merge pull request" e poi "Confirm merge".
5. Allineare il computer locale ed eliminare il branch:
    git switch main
    git pull
    git branch -d feature-analisi-dati

Metodo 2: Tramite terminale (CLI)
    # Torna sul main e assicurati che sia aggiornato
    git switch main
    git pull

    # Mostra le branches attive al momento
    git branches -a

    # Esegui il merge del branch completato
    git merge feature-analisi-dati

    # Invia l'unione a GitHub
    git push origin main

    # Elimina il branch locale non piu necessario
    git branch -d feature-analisi-dati

---

## 5. Risoluzione problemi frequenti

Errore [rejected] - non-fast-forward durante il push:
Qualcuno ha inviato modifiche prima di te:
    git pull --rebase origin main
    git push origin main

Conflitti durante il pull:
Se lo stesso file di testo e stato modificato contemporaneamente:
1. Apri il file segnalato come CONFLICT nell'editor.
2. Risolvi il conflitto rimuovendo i marcatori <<<<<<<, ======= e >>>>>>>.
3. Concludi la sincronizzazione:
    git add file_risolto
    git rebase --continue
    git push origin main
