# ER-diagram: Filmuthyrningsföretag

Nedan visas den konceptuella datamodellen för verksamheten.

```mermaid
erDiagram
    BUTIK ||--|{ ANSTÄLLD : anställer
    BUTIK ||--|{ MEDLEM : registrerar
    
    FILM ||--|{ FILM_GENRE : har
    GENRE ||--|{ FILM_GENRE : tilldelas
    
    FILM ||--|{ FILM_PERSONAL_ROLL : har
    FILMARBETARE ||--|{ FILM_PERSONAL_ROLL : utför
    
    BUTIK ||--|{ BUTIK_FILM : lagerför
    FILM ||--|{ BUTIK_FILM : finns_i
    
    MEDLEM ||--o{ UTHYRNING : registreras_på
    BUTIK_FILM ||--o{ UTHYRNING : hyrs_ut_via
    
    MEDLEM ||--o{ RESERVATION : gör
    BUTIK_FILM ||--o{ RESERVATION : reserveras_i

    BUTIK {
        int ButikID PK
        string Namn
        string Telefon
        string Gata
        string Husnummer
        string Postnummer
        string Stad
    }
    ANSTÄLLD {
        int Anställningsnr PK
        int ButikID FK
        string Namn
        float Lön
        string Roll
    }
    MEDLEM {
        int Medlemsnr PK
        int ButikID FK
        string Namn
        string Adress
        date Startdatum
    }
    FILM {
        int Filmnr PK
        string Titel
        int Längd
    }
    GENRE {
        string Genrenamn PK
    }
    FILM_GENRE {
        int Filmnr FK
        string Genrenamn FK
    }
    FILMARBETARE {
        int PersonID PK
        string Namn
    }
    BUTIK_FILM {
        int ButikID FK
        int Filmnr FK
        float Hyrpris
        string Hylla
        int AntalKopior
        string Status
        float Medelbetyg
    }
    FILM_PERSONAL_ROLL {
        int Filmnr FK
        int PersonID FK
        string Roll
    }
    UTHYRNING {
        int UthyrningsID PK
        int Medlemsnr FK
        int ButikID FK
        int Filmnr FK
        date Uthyrningsdatum
        date Återlämningsdatum
        int Betyg
        date Betygsdatum
    }
    RESERVATION {
        int ReservationsID PK
        int Medlemsnr FK
        int ButikID FK
        int Filmnr FK
        date Registreringsdatum
        date SistaDatum
    }