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

- id_dipartimento
- nome
- descrizione

### CorsiLaurea

- id_corso_laurea
- nome
- livello
- id_dipartimento

### Corsi

- id_corso
- nome
- cfu
- anno_di_corso
- id_corso_di_laurea

### Insegnanti

- id_insegnante
- nome
- cognome
- email

### CorsiInsegnanti

- id_corso
- id_insegnante

### AppelliEsame

- id_appello
- data_appello
- aula
- id_corso

### Studenti

- id_studente
- nome
- cognome
- matricola
- email
- id_corso_di_laurea

### IscrizioniEsami

- id_studente
- id_appello
- voto
- esito
