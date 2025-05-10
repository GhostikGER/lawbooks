# MDT-Lawbooks / MDT-Gesetzbücher

## Description / Beschreibung

**EN:**  
MDT-Lawbooks is a simple FiveM resource that displays your “law books” in-game via a responsive HTML/JavaScript/CSS UI. All data is read from two MySQL tables managed by the **myEmergency** asset (by MG-Scripts). Without **myEmergency**, no tables exist, so you’d have to create and populate them yourself.

**DE:**  
MDT-Lawbooks ist ein FiveM-Resource, das Deine Gesetzbücher im Spiel über eine responsive HTML/JavaScript/CSS-UI anzeigt. Alle Daten werden aus zwei MySQL-Tabellen gelesen, die vom **myEmergency**-Asset (von MG-Scripts) erstellt und befüllt werden. Ohne **myEmergency** existieren die Tabellen nicht – Du müsstest sie dann selbst anlegen und befüllen.

---

## Requirements / Voraussetzungen

- FiveM server (cerulean)  
- es_extended  
- oxmysql  
- ox_lib  
- **myEmergency** by MG-Scripts

---

## Installation / Installation

1. Kopiere den Ordner `MDT-Lawbooks` in Dein `resources`-Verzeichnis.  
2. Füge in `server.cfg` eine Zeile hinzu:  
   ```
   ensure MDT-Lawbooks
   ```
3. Starte oder starte den Server neu.

---

## Configuration / Konfiguration

Alle Einstellungen findest Du in **config.lua**:

```lua
Config = {}

-- Überschrift im UI (oben mittig)
Config.Header = "Gesetzbuch"

-- Datenbank-Tabellen und Sortier-Einstellungen
Config.Tables = {
  law_books = {
    name         = "myemergency_law_books",      -- Tablename
    order        = "id",                         -- Sortier-Spalte
    sorting_type = "ASC"                         -- ASC oder DESC
  },
  law_book_laws = {
    name         = "myemergency_law_book_laws",  -- Tablename
    order        = "paragraph",                  -- Sortier-Spalte
    sorting_type = "ASC"                         -- ASC oder DESC
  }
}

-- NPC-Standorte und Blip-Settings
Config.Locations = {
  {
    coords   = { x=440.98, y=-978.79, z=30.69, h=179.55 },
    pedModel = "a_m_m_business_01",
    blip     = {
      enabled = true, sprite = 77, scale = 0.8, color = 3,
      name    = "Lawbook"
    }
  },
  {
    coords   = { x=117.06, y=-747.30, z=45.75, h=115.18 },
    pedModel = "a_m_m_business_01",
    blip     = {
      enabled = true, sprite = 77, scale = 0.8, color = 3,
      name    = "Lawbook"
    }
  },
}

-- Titel-Template für jedes Gesetzbuch
Config.LawBookName = "{bookID} – {bookName} ({bookShortName})"
```

**DE:**  
- **Header:** Überschrift im NUI.  
- **Tables:** Definiert, aus welchen MySQL-Tabellen (`name`) und nach welchen Spalten (`order`) in welcher Reihenfolge (`sorting_type`) die Daten gelesen werden.  
- **Locations:** Legt NPC-Positionen, Model und Blip-Einstellungen fest.  
- **LawBookName:** Template für den Accordion-Titel im UI.

---

## Usage / Nutzung

1. Bei Spielstart spawnen die Peds an den in `Config.Locations` definierten Koordinaten.  
2. Gehe zum NPC, drücke **E**, um das Gesetzbuch-UI zu öffnen.  
3. Im UI kannst Du jedes Buch aufklappen, nach Paragraph, Titel, Inhalt, Strafe oder Änderungsdatum durchsuchen.  
4. Zum Schließen klick auf das rote **X** oben rechts.

---

## Database / Datenbank

Die Tabellen **myemergency_law_books** und **myemergency_law_book_laws** werden vom **myEmergency**-Asset angelegt und befüllt.  
- **myemergency_law_books**: Spalten `id`, `name`, `short_name`, …  
- **myemergency_law_book_laws**: Spalten `lawbook_id`, `paragraph`, `crime`, `others`, `minimum_penalty`, `detention_time`, `changeddate`, …

Ohne myEmergency musst Du selbst zwei Tabellen mit denselben Spalten anlegen und Daten einfügen.

---

## Future Plans / Zukünftige Erweiterungen

- Suche über alle Bücher hinweg  
- Mehrsprachige UI-Option (aktuell nur DE)  
- Live-Updates bei Datenbank-Änderungen  
- Export-/Druckfunktion für offline-Logs

---

*Made with ❤ by MG-Scripts*  
*Erstellt von MG-Scripts*
