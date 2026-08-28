# Prikupljanje podataka o britpop muzici korišćenjem LLM-ova

**Završni rad - Fakultet organizacionih nauka, Univerzitet u Beogradu**

## O radu

Rad kritički poredi veliki jezički model (LLM) i tri tradicionalna, dokumentovana izvora podataka u zadatku prikupljanja strukturiranih podataka o britpop muzici. Cilj je da se utvrdi da li LLM, bez direktnog pristupa spoljnom izvoru, može pouzdano da generiše precizne podatke o pesmama, u poređenju sa pristupima zasnovanim na API servisima i web scraping-u. Prikupljeni podaci potom su iskorišćeni za deskriptivnu i eksplorativnu analizu žanra.

**Istraživačko pitanje:** Može li veliki jezički model pouzdano da zameni tradicionalne, dokumentovane izvore u zadatku prikupljanja preciznih, činjeničnih podataka o muzici?

## Metodologija

| Pristup | Izvor | Status | Rezultat |
|---|---|---|---|
| Upiti velikom jezičkom modelu | Gemini | Isključeno | Nepouzdano — isti upit poslat dva puta dao je različite rezultate (odstupanje tempa do 62 BPM) |
| Spotify Extended Audio Features API | RapidAPI | Uključeno | 9.024 -> 2.145 pesama posle čišćenja duplikata |
| MusicBrainz | musicbrainzngs | Uključeno | 99,4% pesama uspešno povezano po nazivu i izvođaču |
| AllMusic | web scraping | Uključeno | 2.313 pesama, bez API-ja |

Tri uspešna izvora objedinjena su uz strogo pravilo: u finalnom skupu ostaju isključivo pesme kod kojih su sva tri izvora uspešno povezana.

## Finalni skup podataka

`britpop.csv` sadrži **1.630 pesama**, **22 izvođača** i **160 albuma** (1964–2025), sa kolonama iz sva tri izvora: osnovni metapodaci i audio karakteristike (Spotify), podaci o izvođaču (MusicBrainz) i kategoričke oznake - žanr, stil, raspoloženje, tema (AllMusic).

## Ključni nalazi

- LLM pristup nije pouzdan za prikupljanje preciznih, brojčanih podataka - model generiše vrednosti statistički, ne preuzimanjem stvarnih podataka.
- Dokumentovani pristupi (API, web scraping) ostaju dosledno pouzdan izbor, uprkos većem metodološkom naporu.
- Popularnost pesama ne korelira ni sa jednom audio karakteristikom (svi koeficijenti između −0,03 i 0,05) - trenutnu slušanost oblikuju faktori izvan zvučne strukture snimka.
- Skup podataka je unutrašnje konzistentan sa poznatim obeležjima britpop žanra (prosečna energija 0,70, 70% pesama u durskom tonalitetu).

## Struktura repozitorijuma

```
diplomski/
├── grafici/                          # Grafici iz analize podataka
│
├── oasis_albumi_gemini.ipynb         # Pristup 1: upiti modelu Gemini
├── definitely_maybe_oasis.csv        # Rezultati dve iteracije + poređenje
├── definitely_maybe_oasis2.csv
│
├── spotify_podaci.ipynb              # Pristup 2: Spotify preko RapidAPI-ja
├── spotify_audio_features.csv        # Sirovi podaci
├── spotify_clean.csv                 # Očišćen skup
│
├── musicbrainz_enrichment.ipynb      # Pristup 3: MusicBrainz
├── musicbrainz.csv
├── musicbrainz_clean.csv
│
├── allmusic.ipynb                    # Pristup 4: web scraping AllMusic-a
├── allmusic_cleaning.ipynb
├── allmusic.csv
├── allmusic_clean.csv
│
├── britpop_merge.ipynb               # Objedinjavanje sva tri izvora
├── britpop_merged.csv
├── britpop_eda.ipynb                 # Finalno čišćenje i analiza
├── britpop.csv                       # FINALNI skup podataka
│
├── requirements.txt
└── .gitignore
```

## Pokretanje projekta

```bash
python -m venv venv
venv\Scripts\activate        # Windows
pip install -r requirements.txt
```

Sveske koje pristupaju spoljnim servisima zahtevaju sopstveni RapidAPI ključ, postavljen kao promenljiva okruženja:

```bash
set RAPIDAPI_KEY=tvoj_kljuc
```

## Napomena o podacima

Skup podataka je namenjen isključivo istraživačkim/akademskim svrhama.
