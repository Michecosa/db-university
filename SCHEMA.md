# DB SCHEMA

Modellizzare la struttura di un database per memorizzare tutti i dati riguardanti una università:

- sono presenti diversi `Dipartimenti` (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);,
- ogni `Dipartimento` offre più `Corsi di Laurea` (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..),
- ogni `Corso di Laurea` prevede diversi `Corsi` (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);,
- ogni `Corso` può essere tenuto da diversi `Insegnanti`;,
- ogni `Corso` prevede più appelli d'Esame;,
- ogni `Studente` è iscritto ad un solo `Corso di Laurea`;,
- ogni `Studente` può iscriversi a più appelli di `Esame`;,
- per ogni appello d'`Esame` a cui lo `Studente` ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente.,
  Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.

## Table name: university (entity name: **_university_**)

### Dipartimenti

- id_dipartimento INT, PRIMARY KEY, AUTO_INCREMENT, NOT NULL
- nome VARCHAR(50), UNIQUE, NOT NULL
- descrizione TEXT, NULL

### CorsiLaurea

- id_corso_laurea INT, PRIMARY KEY, AUTO_INCREMENT, NOT NULL
- nome VARCHAR(50), NOT NULL
- livello VARCHAR(50)
- id_dipartimento INT, NOT NULL, FOREIGN KEY di Dipartimenti(id_dipartimento)

### Corsi

- id_corso INT, PRIMARY KEY, AUTO_INCREMENT, NOT NULL
- nome VARCHAR(50), NOT NULL
- cfu INT, NOT NULL
- anno_di_corso INT, NOT NULL
- id_corso_di_laurea INT, NOT NULL, FOREIGN KEY di CorsiLaurea(id_corso_laurea)

### Insegnanti

- id_insegnante INT, PRIMARY KEY, AUTO_INCREMENT, NOT NULL
- nome VARCHAR(50), NOT NULL
- cognome VARCHAR(50), NOT NULL
- email VARCHAR(50), UNIQUE, NOT NULL

### CorsiInsegnanti

- id_corso INT, NOT NULL, FOREIGN KEY di Corsi(id_corso)
- id_insegnante INT, NOT NULL, FOREIGN KEY di Insegnanti(id_insegnante)
- PRIMARY KEY (id_corso, id_insegnante)

### AppelliEsame

- id_appello INT, PRIMARY KEY, AUTO_INCREMENT, NOT NULL
- data_appello DATE, NOT NULL
- aula VARCHAR(50), NULL
- id_corso INT, NOT NULL, FOREIGN KEY di Corsi(id_corso)

### Studenti

- id_studente INT, PRIMARY KEY, AUTO_INCREMENT, NOT NULL
- nome VARCHAR(50), NOT NULL
- cognome VARCHAR(50), NOT NULL
- matricola VARCHAR(20), UNIQUE, NOT NULL
- email VARCHAR(50), UNIQUE, NOT NULL
- id_corso_di_laurea INT, NOT NULL, FOREIGN KEY di CorsiLaurea(id_corso_laurea)

### IscrizioniEsami

- id_studente INT, NOT NULL, FOREIGN KEY di Studenti(id_studente)
- id_appello INT, NOT NULL, FOREIGN KEY di AppelliEsame(id_appello)
- voto TINYINT, NULL
- esito VARCHAR(20), NOT NULL
- PRIMARY KEY (id_studente, id_appello)
