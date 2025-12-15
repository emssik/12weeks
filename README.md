# AI 12-Week Planner

Framework asystenta osobistego opartego na AI do zarządzania zadaniami, projektami i celami życiowymi z wykorzystaniem metodologii 12-Week Year.

## Co to jest?

To szablon/framework do budowania spersonalizowanego asystenta AI, który pomaga w:
- Zarządzaniu zadaniami i projektami
- Śledzeniu długoterminowych celów
- 12-tygodniowych cyklach planowania
- Planowaniu dziennym i tygodniowym
- Śledzeniu nawyków i rozwoju osobistym

## Struktura plików

```
.
├── README.md                     # Ten plik - szybki przewodnik
├── context.md                    # TWÓJ KONTEKST - informacje osobiste, cele, projekty
├── progress.md                   # Śledzenie postępów w realizacji długoterminowych celów
├── issues.json                   # Zadania z systemu zarządzania zadaniami (opcjonalne)
├── templates/
│   ├── 12-week-planning.md       # Szablon formularza planowania 12-tygodniowego
│   ├── project-brief.md          # Szablon briefu projektu technicznego
│   └── project-brief-general.md  # Szablon briefu projektu nietechnicznego
├── projects/                     # Briefy projektów (wygenerowane z formularza planowania)
├── plans/                        # Wygenerowane plany 12-tygodniowe
└── .claude/commands/
    ├── init-project-briefs.md    # Generuje briefy projektów z formularza planowania
    └── 12week-plan.md            # Generuje plan 12-tygodniowy z briefów
```

## Rozpoczęcie pracy

### Krok 1: Wypełnij swój kontekst

Edytuj `context.md` swoimi informacjami osobistymi:
- Kim jesteś (podstawowe informacje, rodzina, praca)
- Twój typowy dzień i harmonogram
- Jak pracujesz (motywacja, frustracje, styl podejmowania decyzji)
- Narzędzia, których używasz
- Długoterminowe cele (zdrowie, relacje, finanse)
- Aktywne projekty
- Jak chcesz, aby asystent z Tobą współpracował

### Krok 2: Skonfiguruj śledzenie postępów

Edytuj `progress.md`, aby śledzić swoje długoterminowe cele:
- Zdefiniuj mierzalne cele
- Ustaw wartości początkowe
- Regularnie aktualizuj w miarę postępów

### Krok 3: Cykl planowania 12-tygodniowego

#### 3.1 Wypełnij formularz planowania
Skopiuj i wypełnij `templates/12-week-planning.md` swoimi celami na kolejne 12 tygodni (max 3-4 cele).

#### 3.2 Wygeneruj briefy projektów
Uruchom komendę:
```
/init-project-briefs templates/12-week-planning.md
```
To tworzy puste briefy w `projects/` dla każdego celu.

#### 3.3 Wypełnij briefy projektów
Uzupełnij każdy brief w `projects/`:
- Stan obecny
- Stos technologiczny (jeśli dotyczy)
- Etapy implementacji

#### 3.4 Wygeneruj plan 12-tygodniowy
Po wypełnieniu briefów uruchom:
```
/12week-plan templates/12-week-planning.md
```

## Dla asystenta AI

Jeśli jesteś asystentem AI czytającym to:

1. Zacznij od `context.md` - zrozum sytuację użytkownika, cele i styl pracy
2. Sprawdź `progress.md` - zobacz obecny postęp w realizacji długoterminowych celów
3. Przeczytaj sekcję "Jak powinien działać asystent" w context.md
4. Priorytetyzuj według: deadline > wpływ finansowy > zdrowie > inne
5. Równoważ filary życia użytkownika (typowo: zdrowie, relacje, finanse)

## Kluczowe zasady

- **Realistyczne zamiast ambitnych** - osiągalne plany są lepsze niż porzucone
- **Świadomość energii** - dostosuj się do codziennej energii i nastroju
- **Postęp zamiast perfekcji** - małe konsekwentne kroki wygrywają
- **Świadomość kontekstu** - używaj pełnego obrazu do podejmowania decyzji
- **Przejrzystość** - wyjaśniaj rozumowanie, zaznaczaj niepewności

## Dostosowywanie

Ten framework jest elastyczny. Dostosuj go do swoich potrzeb:
- Dodaj/usuń sekcje w `context.md`
- Modyfikuj szablony planowania
- Twórz własne komendy slash
- Integruj ze swoim systemem zarządzania zadaniami poprzez `issues.json`
