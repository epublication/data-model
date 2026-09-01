# Migrationsdokumentation: SHAB → ePublication (Meldungstypen-Mapping)

> **Kontext:** ePublication (Swiss Official Gazettes Portal) löst das bisherige
> Amtsblattportal ab, über das amtliche Publikationen (Meldungen) verschiedener
> Gemeinwesen auf den drei föderalen Stufen der Schweiz (Bund, Kantone, Gemeinden)
> veröffentlicht wurden. Auf Stufe Bund betrifft dies insbesondere das **SHAB**
> (Schweizerisches Handelsamtsblatt). Auf ePublication werden Meldungen mit einer
> **einfacheren, generischeren Struktur** publiziert als bisher auf dem
> Amtsblattportal.

---

## Kanonische Quelle

Die vollständigen, laufend gepflegten Mapping-Tabellen (bisherige SHAB-Rubriken/
Unterrubriken → neue Meldungstypen) werden **nicht** in diesem Repository
dupliziert, sondern zentral im Help Center gepflegt, um Redundanz und
veraltete Kopien zu vermeiden:

- 🇩🇪 Deutsch: [Amtsblätter der Plattform](https://helpcenter-epublication.zendesk.com/hc/de/articles/29956526113052-Amtsbl%C3%A4tter-der-Plattform)
- 🇫🇷 Français: [Bulletins officiels de la plateforme](https://helpcenter-epublication.zendesk.com/hc/fr/articles/29956526113052-Bulletins-officiels-de-la-plateforme)
- 🇮🇹 Italiano: [Gazzette ufficiali della piattaforma](https://helpcenter-epublication.zendesk.com/hc/it/articles/29956526113052-Gazzette-ufficiali-della-piattaforma)

> Diese Seite existiert **nicht auf Englisch**. Englischsprachige Leser:innen
> müssen auf eine der drei Sprachvarianten ausweichen.

Von dort aus ist pro Amtsblatt die zugehörige Excel-Mappingtabelle als Download
verlinkt, u. a. für das **Schweizerische Handelsamtsblatt (SHAB)**. Für die
meisten kantonalen Amtsblätter sind die Mappingtabellen laut Seite noch nicht
publiziert ("Mappingtabelle folgt...") – Stand siehe jeweils die Seite selbst.

> **Hinweis:** Diese Mapping-Tabellen befinden sich laut Help Center noch in
> Bearbeitung und werden laufend ergänzt/angepasst. Für den verbindlichen,
> aktuellen Stand daher immer die Help-Center-Seite konsultieren, nicht eine
> lokale Kopie.

---

## Bekannte offene Punkte (aus einer früheren Analyse)

Bei einer früheren Analyse einer Zwischenversion der SHAB-Mappingtabelle sind
folgende Punkte aufgefallen, die bei der Migration zu beachten sind. Da sich
die kanonische Tabelle laufend ändert, sollte jeder Punkt gegen den
**aktuellen** Stand im Help Center verifiziert werden – die folgenden Punkte
könnten mittlerweile überholt sein:

- **Unklare Zuordnung bei `SB05`** (Bereinigung des Eigentumsvorbehaltsregisters):
  In einer früheren Version enthielt die Meldungstyp-Spalte für dieses Kürzel
  einen Zusatz zu Typ `213` ("Grundbucheinführung") mit einem Fragezeichen,
  was auf eine noch ungeklärte Zuordnung hindeutete.
- **Rechtstexte, die nicht mehr automatisch bereitgestellt werden:** Für
  mehrere Kürzel im Bereich Handelsregisterverordnung war vermerkt, dass der
  bisher vom Amtsblattportal bereitgestellte Rechtstext künftig **nicht mehr**
  automatisch zur Verfügung steht. Fachapplikationen, die sich bisher darauf
  verlassen haben, müssten diesen künftig selbst mitliefern.
- **Wegfall von Radiobuttons/Einzelfeldern zugunsten von Freitext:** An
  mehreren Stellen (z. B. Kapitalherabsetzung) wurde vermerkt, dass frühere
  Radiobutton-Auswahlen wegfallen und entsprechende Rechtstexte künftig selbst
  definiert werden müssen statt aus einer vorgegebenen Auswahl zu stammen.

---

## Praktischer Hinweis zur Nutzung

Für die technische Umsetzung eines gefundenen Meldungstyps (Felder,
`valueTypeConfig`, Geschäftsfälle) ist die Mapping-Tabelle nur ein
Startpunkt. Verbindlich ist die Live-Definition über die API:

```http
GET /public/interface/v1/announcement-types/{announcementTypeId}
```

Siehe [Announcement Export](announcement-export.md), Abschnitt 7, für Details
zu diesem und weiteren Referenzdaten-Endpunkten.

---

## Support & weiterführende Links

- [Announcement Import](announcement-import.md) – separates Dokument
- [Announcement Export](announcement-export.md) – separates Dokument
- Fachliches Grundlagendokument: [Standardisierte Meldungstypen](https://helpcenter-epublication.zendesk.com/hc/de/articles/28970270476572-Standardisierte-Meldungstypen) (Deutsch)
