Modellare la struttura di un database per memorizzare tutti i dati riguardanti una università:

- sono presenti diversi **Dipartimenti** (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);

- ogni **Dipartimento** offre più **Corsi di Laurea** (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)

- ogni **Corso di Laurea** prevede diversi **Corsi** (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);

- ogni **Corso** può essere tenuto da diversi **Insegnanti**;

- ogni **Corso** prevede più appelli d'**Esame**;

- ogni **Studente** è iscritto ad un solo **Corso di Laurea**;

- ogni **Studente** può iscriversi a più appelli di **Esame**;

- per ogni appello d'**Esame** a cui lo **Studente** ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente. Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.

## Structure :
- Dipartimenti
- Corsi_di_Laurea
- Corsi
- Insegnati 
- Esami 
- Studenti 
- Partecipazioni 

## Dipartimenti :
- ID | BIGINT - AUTO-INCREMENT - PRIMARY_KEY (UNIQUE, NOTNULL)
- NOME | VARCHAR(20) - NOT NULL
- DESCRIZIONE | TEXT - NULL

## Corsi_di_Laurea :
- ID | BIGINT - AUTO-INCREMENT - PRIMARY_KEY (UNIQUE, NOTNULL)
- NOME | VARCHAR(20) - NOT NULL
- Dipartimento_id 

## Corsi :
- ID | BIGINT - AUTO-INCREMENT - PRIMARY_KEY (UNIQUE, NOTNULL)
- NOME | VARCHAR(20) - NOT NULL
- DATA | DATE
- Corso_di_Laurea_id

## Insegnanti :
- ID | BIGINT - AUTO-INCREMENT - PRIMARY_KEY (UNIQUE, NOTNULL)
- NOME | VARCHAR(20) - NOT NULL
- COGNONME | VARCHAR(20) - NOT NULL

## Esami :
- ID | BIGINT - AUTO-INCREMENT - PRIMARY_KEY (UNIQUE, NOTNULL)
- NOME | VARCHAR(20) - NOT NULL
- DATA | DATE

## Studenti :
- ID | BIGINT - AUTO-INCREMENT - PRIMARY_KEY (UNIQUE, NOTNULL)
- NOME | VARCHAR(20) - NOT NULL
- COGNONME | VARCHAR(20) - NOT NULL
- MATRICOLA | VARCHAR(30) - NOT NULL - UNIQUE
- Corso_di_Laurea_id

## Partecipazioni :
- Studente_id
- Esame_id
- VOTO | VARCHAR(20) - NOT NULL
- STATO | VARCHAR(20) - NOT NULL