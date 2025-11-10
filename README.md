# App4KITAs Dashboard - Vollständige Funktionalitäts-Dokumentation

**Letzte Aktualisierung: October 2025**  

---

## 📋 Inhaltsverzeichnis

- [Übersicht](#übersicht)
- [Super Admin Dashboard Seiten](#super-admin-dashboard-seiten)
- [Träger Admin Dashboard Seiten](#träger-admin-dashboard-seiten)
- [Admin Dashboard Seiten](#admin-dashboard-seiten)
- [Educator Dashboard Seiten](#educator-dashboard-seiten)
- [Gemeinsame Komponenten](#gemeinsame-komponenten)
- [API Services](#api-services)

---

## Übersicht

Das App4KITAs Dashboard ist eine React-basierte Web-Anwendung mit rollenbasierter Zugriffskontrolle. Das Dashboard besteht aus **29 Seiten** über 4 Benutzerrollen hinweg, mit umfassender Funktionalität zur Verwaltung von Kindertagesstätten, Kindern, Personal und Kommunikation.

### Rollen-Übersicht

| Rolle | Seiten | Beschreibung |
|------|-------|-------------|
| **SUPER_ADMIN** | 8 Seiten | Plattform-weite Administration |
| **TRAGER_ADMIN** | 5 Seiten | Organisationsebene-Verwaltung |
| **ADMIN** | 11 Seiten | Institutionsebene-Verwaltung |
| **EDUCATOR** | 5 Seiten | Tägliche Betriebsabläufe und Kinderbetreuung |

**Gesamt: 29 Seiten**

---

## Super Admin Dashboard Seiten

### 1. Dashboard (`/super-admin/dashboard`)

**Datei:** `pages/super_admin/Dashboard.tsx`

**Funktionalität:**
- **Plattform-Statistiken:**
  - Gesamtanzahl Träger (Organisationen)
  - Gesamtanzahl Institutionen
  - Gesamtanzahl Benutzer (alle Rollen)
  - Aktive Benutzer
  - Inaktive Benutzer

- **Schnellzugriffe:**
  - Träger-Verwaltung
  - Institutionen-Verwaltung
  - Statistiken
  - Berichte
  - Erzieher-Verwaltung
  - Eltern-Verwaltung
  - GDPR-Compliance

- **Aktivitätsprotokoll:**
  - Aktuelle Plattform-Aktivitäten
  - System-weite Ereignisse
  - Aktivitäts-Zeitstrahl

- **Persönliches Notizbuch:**
  - Private Notizen für Super Admin

**API-Aufrufe:**
- `getSuperAdminStats()` - Plattform-Statistiken
- Aktivitätsprotokoll-Abruf

---

### 2. Träger-Verwaltung (`/super-admin/traeger`)

**Datei:** `pages/super_admin/Traeger.tsx`

**Funktionalität:**
- **Träger CRUD:**
  - Träger (Organisation) erstellen
  - Träger-Informationen bearbeiten
  - Träger löschen
  - Träger-Details anzeigen

- **Träger-Informationen:**
  - Name
  - Adresse
  - Kontakt-E-Mail
  - Kontakt-Telefon
  - Erstellt von (Super Admin)
  - Erstellungsdatum

- **Träger-Admin-Verwaltung:**
  - Träger-Admin-Benutzer erstellen
  - Träger-Admin-Informationen bearbeiten
  - Träger-Admin löschen
  - Träger-Admin einem Träger zuweisen
  - Alle Träger-Admins anzeigen

- **Träger-Admin-Informationen:**
  - Name, E-Mail
  - Passwort-Verwaltung
  - Träger-Zuordnung
  - Status (aktiv/inaktiv)
  - Letzter Login

- **Suche & Filter:**
  - Träger nach Name suchen
  - Träger-Admins suchen
  - Paginierung

**API-Aufrufe:**
- `getAllTraeger()` - Alle Träger auflisten
- `createTraeger()` - Träger erstellen
- `updateTraeger()` - Träger aktualisieren
- `deleteTraeger()` - Träger löschen
- `getAllTraegerAdmins()` - Alle Träger-Admins auflisten
- `createTraegerAdmin()` - Träger-Admin erstellen
- `updateTraegerAdmin()` - Träger-Admin aktualisieren
- `deleteTraegerAdmin()` - Träger-Admin löschen
- `fetchAllUsers()` - Alle Benutzer abrufen
- `updateUserStatus()` - Benutzerstatus aktualisieren

---

### 3. Institutionen (`/super-admin/institutionen`)

**Datei:** `pages/super_admin/Institutionen.tsx`

**Funktionalität:**
- **Institution CRUD:**
  - Institution erstellen
  - Institution bearbeiten
  - Institution löschen
  - Institutions-Details anzeigen

- **Institutions-Informationen:**
  - Name, Adresse
  - Träger-Zuordnung (erforderlich)
  - Öffnungszeiten
  - Kontaktinformationen
  - Einstellungen

- **Institutions-Statistiken:**
  - Anzahl Kinder
  - Anzahl Gruppen
  - Anzahl Erzieher
  - Aktivitäts-Metriken

- **Suche & Filter:**
  - Nach Name suchen
  - Nach Träger filtern
  - Paginierung

**API-Aufrufe:**
- Institutions-Verwaltungs-APIs
- Statistiken-APIs

---

### 4. Statistiken (`/super-admin/statistiken`)

**Datei:** `pages/super_admin/Statistiken.tsx`

**Funktionalität:**
- **Plattform-weite Statistiken:**
  - Benutzerwachstum über Zeit
  - Aktive Benutzer
  - Check-in-Trends
  - Nachrichten-Volumen
  - Benachrichtigungs-Statistiken
  - Fehlgeschlagene Logins
  - Gruppen-Anwesenheit
  - Check-in-Methoden

- **Diagramme & Visualisierungen:**
  - Benutzerwachstums-Diagramme
  - Aktivitäts-Trends
  - Plattform-weite Metriken
  - Vergleichende Analysen

- **Datumsbereich-Filterung:**
  - Benutzerdefinierte Datumsbereiche
  - Zeitraum-Auswahl
  - Export-Funktionen

**API-Aufrufe:**
- `getSuperAdminStats()` - Plattform-Statistiken
- Verschiedene Analytics-APIs

---

### 5. Berichte (`/super-admin/reports`)

**Datei:** `pages/super_admin/Reports.tsx`

**Funktionalität:**
- **Plattform-Berichte:**
  - Benutzerwachstums-Bericht
  - Aktive Benutzer-Bericht
  - Check-in-Trends-Bericht
  - Aktive Gruppen-Bericht
  - Nachrichten-Volumen-Bericht
  - Benachrichtigungs-Statistiken-Bericht
  - Fehlgeschlagene Logins-Bericht
  - Gruppen-Anwesenheits-Bericht
  - Check-in-Methoden-Bericht
  - Plattform-Statistiken-Bericht

- **Export-Funktionen:**
  - CSV-Export
  - PDF-Export
  - Massen-Export

**API-Aufrufe:**
- Plattform-Berichts-APIs aus `reportApi.ts`

---

### 6. Erzieher (`/super-admin/educators`)

**Datei:** `pages/super_admin/Educators.tsx`

**Funktionalität:**
- **Plattform-weite Erzieher-Verwaltung:**
  - Alle Erzieher über alle Institutionen hinweg anzeigen
  - Erzieher-Details
  - Institutions-Zuordnung
  - Status-Verfolgung

- **Erzieher-Informationen:**
  - Name, E-Mail, Telefon
  - Institution
  - Gruppen
  - Status (aktiv/inaktiv)
  - Letzter Login

- **Suche & Filter:**
  - Nach Name/E-Mail suchen
  - Nach Institution filtern
  - Nach Status filtern
  - Paginierung

**API-Aufrufe:**
- Plattform-weite Benutzer-APIs

---

### 7. Eltern (`/super-admin/parents`)

**Datei:** `pages/super_admin/Parents.tsx`

**Funktionalität:**
- **Plattform-weite Eltern-Verwaltung:**
  - Alle Eltern über alle Institutionen hinweg anzeigen
  - Eltern-Details
  - Kinder-Zuordnungen
  - Status-Verfolgung

- **Eltern-Informationen:**
  - Name, E-Mail, Telefon
  - Institution
  - Kinder
  - Status (aktiv/inaktiv)
  - Letzter Login

- **Suche & Filter:**
  - Nach Name/E-Mail suchen
  - Nach Institution filtern
  - Nach Status filtern
  - Paginierung

**API-Aufrufe:**
- Plattform-weite Benutzer-APIs

---

### 8. GDPR-Compliance (`/super-admin/gdpr`)

**Datei:** `pages/super_admin/GDPRCompliancePage.tsx`

**Funktionalität:**
- **GDPR-Dashboard:**
  - Audit-Protokolle
  - Ausstehende Löschungen
  - Datenaufbewahrungs-Verwaltung
  - Compliance-Berichte

- **Datenverwaltung:**
  - Datenexport-Anfragen
  - Löschungs-Anfragen
  - Anonymisierung
  - Tiefenbereinigung

- **Compliance-Tools:**
  - Einwilligungs-Verfolgung
  - Datenaufbewahrungs-Fristen
  - Audit-Trail
  - Compliance-Berichte

**API-Aufrufe:**
- GDPR-Verwaltungs-APIs aus `gdprApi.ts`

---

## Träger Admin Dashboard Seiten

### 1. Dashboard (`/traeger-admin/dashboard`)

**Datei:** `pages/traeger_admin/Dashboard.tsx`

**Funktionalität:**
- **Träger-Statistiken:**
  - Gesamtanzahl Kinder (Träger-weit)
  - Kinder >8h Anwesenheit
  - Gesamtanzahl Erzieher
  - Gesamtanzahl Institutionen
  - Inaktive Benutzer (letzte 4 Wochen)
  - Fehlgeschlagene Logins (letzte 30 Tage)

- **Schnellzugriffe:**
  - Einrichtungen-Verwaltung
  - Statistiken
  - Benutzer-Verwaltung
  - Einstellungen

- **Warnungen:**
  - Inaktive Benutzer-Warnung
  - Fehlgeschlagene Login-Warnungen
  - Sicherheits-Benachrichtigungen

**API-Aufrufe:**
- `getTraegerStats()` - Träger-Statistiken
- `getInactiveUsers()` - Inaktive Benutzer
- `getFailedLogins()` - Fehlgeschlagene Logins

---

### 2. Einrichtungen (`/traeger-admin/einrichtungen`)

**Datei:** `pages/traeger_admin/Einrichtungen.tsx`

**Funktionalität:**
- **Institutions-Verwaltung (Träger-weit):**
  - Alle Institutionen im Träger anzeigen
  - Neue Institution erstellen
  - Institution bearbeiten
  - Institution löschen
  - Institutions-Details anzeigen

- **Institutions-Informationen:**
  - Name, Adresse
  - Kontaktinformationen
  - Einstellungen
  - Statistiken pro Institution

- **Institutions-Statistiken:**
  - Anzahl Kinder pro Institution
  - Anzahl Erzieher pro Institution
  - Aktivitäts-Metriken

- **Suche & Filter:**
  - Nach Name suchen
  - Paginierung

**API-Aufrufe:**
- Träger Admin Institutions-APIs

---

### 3. Statistiken (`/traeger-admin/statistiken`)

**Datei:** `pages/traeger_admin/Statistiken.tsx`

**Funktionalität:**
- **Träger-weite Statistiken:**
  - Gesamtanzahl Kinder (alle Institutionen)
  - Kinder >8h (alle Institutionen)
  - Gesamtanzahl Erzieher
  - Pro-Institution Aufschlüsselung
  - Inaktive Benutzer
  - Fehlgeschlagene Logins

- **Diagramme & Visualisierungen:**
  - Träger-weite Trends
  - Pro-Institution Vergleich
  - Aktivitäts-Diagramme

- **Datumsbereich-Filterung:**
  - Benutzerdefinierte Datumsbereiche
  - Export-Funktionen

**API-Aufrufe:**
- Träger Admin Statistiken-APIs

---

### 4. Benutzer (`/traeger-admin/benutzer`)

**Datei:** `pages/traeger_admin/Benutzer.tsx`

**Funktionalität:**
- **Benutzer-Verwaltung (Träger-weit):**
  - Alle Admins und Erzieher im Träger anzeigen
  - Neue Benutzer erstellen (Admin, Erzieher)
  - Benutzer-Informationen bearbeiten
  - Benutzer löschen
  - Benutzer sperren/entsperren

- **Benutzer-Informationen:**
  - Name, E-Mail, Telefon
  - Rolle (ADMIN, EDUCATOR)
  - Institutions-Zuordnung
  - Status (aktiv/inaktiv)
  - Letzter Login

- **Benutzer-Funktionen:**
  - Passwort-Verwaltung
  - Status-Updates
  - Sperren/Entsperren-Funktionalität
  - Inaktive Benutzer-Identifikation

- **Suche & Filter:**
  - Nach Name/E-Mail suchen
  - Nach Rolle filtern
  - Nach Institution filtern
  - Nach Status filtern
  - Paginierung

**Hinweis:** Eltern können nicht vom Träger-Admin verwaltet werden

**API-Aufrufe:**
- Träger Admin Benutzer-Verwaltungs-APIs

---

### 5. Einstellungen (`/traeger-admin/einstellungen`)

**Datei:** `pages/traeger_admin/Einstellungen.tsx`

**Funktionalität:**
- **Träger-Einstellungen:**
  - Träger-Informationen
  - Kontaktdaten
  - Einstellungs-Konfiguration
  - (Platzhalter für zukünftige Features)

**API-Aufrufe:**
- Träger-Einstellungs-APIs

---

## Admin Dashboard Seiten

### 1. Dashboard (`/admin/dashboard`)

**Datei:** `pages/admin/Dashboard.tsx`

**Funktionalität:**
- **Statistik-Übersicht:**
  - Gesamtanzahl Kinder
  - Gesamtanzahl Gruppen
  - Gesamtanzahl Erzieher
  - Heutige Check-ins
  - Ausstehende Check-ins (Kinder noch nicht eingecheckt)
  - Aktuelle Aktivitäts-Feed
  - Schnellzugriffs-Karten zu wichtigen Funktionen

- **Schnellzugriffe:**
  - Kinder-Verwaltung
  - Gruppen-Verwaltung
  - Personal-Verwaltung
  - Statistiken
  - Berichte
  - Kalender & Veranstaltungen
  - Kommunikation
  - Chat

- **Persönliches Notizbuch:**
  - Private Notizen für Admin
  - Persistente Speicherung
  - Schnellzugriff vom Dashboard

- **Aktuelle Aktivitäten:**
  - Letzte Check-ins/outs
  - Aktuelle Updates
  - Aktivitäts-Zeitstrahl

**API-Aufrufe:**
- `getAdminStats()` - Dashboard-Statistiken
- Aktivitätsprotokoll-Abruf

---

### 2. Kinder-Verwaltung (`/admin/children`)

**Datei:** `pages/admin/Children.tsx`

**Funktionalität:**
- **CRUD-Operationen:**
  - Neues Kind mit vollständigem Profil erstellen
  - Kind-Informationen bearbeiten
  - Kind löschen (Soft Delete)
  - Kind-Details anzeigen

- **Kind-Profil-Felder:**
  - Name, Geburtsdatum
  - Foto-Upload und -Verwaltung
  - Allergien und medizinische Bedingungen
  - Notfallkontakt-Informationen
  - Gruppen-Zuordnung
  - Eltern-Zuordnungen (mehrere Eltern)
  - Einwilligungs-Verwaltung (Foto, Datenverarbeitung, Marketing)

- **QR-Code-Verwaltung:**
  - QR-Code für einzelnes Kind generieren
  - Bulk-QR-Code-Generierung für mehrere Kinder
  - QR-Code PDF-Export
  - QR-Code Druck-Status-Verfolgung
  - QR-Codes neu generieren

- **Foto-Verwaltung:**
  - Kinderfotos hochladen
  - Foto-Vorschau
  - Foto-Löschung

- **Eltern-Verwaltung:**
  - Mehrere Eltern einem Kind zuweisen
  - Eltern-Zuordnungen entfernen
  - Eltern-Informationen anzeigen

- **Suche & Filter:**
  - Nach Name suchen
  - Nach Gruppe filtern
  - Nach Einwilligungs-Status filtern
  - Paginierung

**API-Aufrufe:**
- `fetchChildren()` - Alle Kinder auflisten
- `addChild()` - Kind erstellen
- `editChild()` - Kind aktualisieren
- `deleteChild()` - Kind löschen
- `fetchChildQRCode()` - QR-Code abrufen
- `uploadChildPhoto()` - Foto hochladen
- `fetchGroups()` - Gruppen für Zuordnung abrufen
- `fetchParents()` - Eltern für Zuordnung abrufen

---

### 3. Gruppen-Verwaltung (`/admin/groups`)

**Datei:** `pages/admin/Groups.tsx`

**Funktionalität:**
- **CRUD-Operationen:**
  - Neue Gruppe erstellen
  - Gruppen-Informationen bearbeiten
  - Gruppe löschen
  - Gruppen-Details anzeigen

- **Gruppen-Informationen:**
  - Gruppenname
  - Gruppenbeschreibung
  - Institutions-Zuordnung

- **Erzieher-Zuordnung:**
  - Mehrere Erzieher einer Gruppe zuweisen
  - Erzieher aus Gruppe entfernen
  - Zugewiesene Erzieher anzeigen
  - Erzieher-Anzahl pro Gruppe

- **Kinder-Zuordnung:**
  - Kinder in Gruppe anzeigen
  - Kinder-Anzahl pro Gruppe
  - (Kinder-Zuordnung wird auf Kinder-Seite verwaltet)

- **Gruppen-Statistiken:**
  - Anzahl Kinder
  - Anzahl Erzieher
  - Gruppen-Aktivitäts-Status

- **Suche & Filter:**
  - Nach Name suchen
  - Paginierung

**API-Aufrufe:**
- `fetchGroups()` - Alle Gruppen auflisten
- `addGroup()` - Gruppe erstellen
- `editGroup()` - Gruppe aktualisieren
- `deleteGroup()` - Gruppe löschen
- `fetchEducators()` - Erzieher für Zuordnung abrufen
- `assignEducators()` - Erzieher Gruppe zuweisen
- `updateGroupEducators()` - Erzieher-Zuordnungen aktualisieren

---

### 4. Personal-Verwaltung (`/admin/personal`)

**Datei:** `pages/admin/Personal.tsx`

**Funktionalität:**
- **CRUD-Operationen:**
  - Neuen Erzieher/Mitarbeiter erstellen
  - Mitarbeiter-Informationen bearbeiten
  - Mitarbeiter löschen
  - Mitarbeiter-Details anzeigen

- **Mitarbeiter-Profil-Felder:**
  - Name, E-Mail, Telefon
  - Rolle (EDUCATOR, ADMIN)
  - Status (aktiv, inaktiv, gesperrt)
  - Gruppen-Zuordnungen
  - Letzter Login Zeitstempel
  - Avatar-Upload

- **Status-Verwaltung:**
  - Mitarbeiter aktivieren/deaktivieren
  - Mitarbeiter-Konten sperren
  - Status-Badges mit visuellen Indikatoren

- **Passwort-Verwaltung:**
  - Erzieher-Passwort ändern (Admin-Funktion)
  - Passwort-Reset-Funktionalität

- **Gruppen-Zuordnung:**
  - Mitarbeiter Gruppen zuweisen
  - Gruppen-Mitgliedschaften anzeigen
  - Mehrfache Gruppen-Zuordnungen

- **Aktivitäts-Verfolgung:**
  - Letzte Login-Zeit
  - Konto-Status-Historie
  - Aktivitäts-Indikatoren

- **Suche & Filter:**
  - Nach Name oder E-Mail suchen
  - Nach Rolle filtern
  - Nach Status filtern
  - Paginierung

**API-Aufrufe:**
- `fetchEducators()` - Alle Erzieher auflisten
- `addEducator()` - Erzieher erstellen
- `editEducator()` - Erzieher aktualisieren
- `deleteEducator()` - Erzieher löschen
- `changeEducatorPassword()` - Passwort ändern
- `updateUserStatus()` - Status aktualisieren
- `fetchGroups()` - Gruppen für Zuordnung abrufen

---

### 5. Statistiken (`/admin/statistiken`)

**Datei:** `pages/admin/Statistiken.tsx`

**Funktionalität:**
- **Übersichts-Statistiken:**
  - Gesamtanzahl Kinder
  - Gesamtanzahl Gruppen
  - Gesamtanzahl Erzieher
  - Heutige Check-ins
  - Kinder >8h Anwesenheit
  - Aktuelle Aktivitäts-Anzahl

- **Diagramme & Visualisierungen:**
  - 7-Tage-Anwesenheits-Trend (Liniendiagramm)
  - Gruppen-weise Anwesenheit (Balkendiagramm)
  - Check-in/out-Muster (Flächendiagramm)
  - Zeitbasierte Analysen

- **Gruppen-Statistiken:**
  - Pro-Gruppe Anwesenheitsraten
  - Gruppen-Leistungs-Metriken
  - Gruppen-Vergleichs-Diagramme

- **Check-in-Statistiken:**
  - Tägliche Check-in-Anzahlen
  - Check-in-Methoden (QR vs. Manuell)
  - Check-in-Zeit-Verteilung
  - Verspätungs-Verfolgung

- **Echtzeit-Updates:**
  - Live-Statistik-Aktualisierung
  - Datumsbereich-Filterung
  - Export-Funktionen

**API-Aufrufe:**
- `getAdminStats()` - Gesamt-Statistiken
- `fetchCheckinStats()` - Check-in-Statistiken
- `fetchGroups()` - Gruppendaten für Diagramme

---

### 6. Berichte (`/admin/reports`)

**Datei:** `pages/admin/Reports.tsx`

**Berichtstypen (8 insgesamt):**

#### 6.1 Tagesbericht (`DailyReport.tsx`)
- Heutige Anwesenheits-Zusammenfassung
- Check-ins/outs für den Tag
- Verspätete Ankünfte
- Verspätete Abholungen
- Abwesenheiten
- CSV/PDF-Export

#### 6.2 Monatsbericht (`MonthlyReport.tsx`)
- Monatliche Anwesenheits-Trends
- Monatliche Statistiken
- Vergleich mit Vormonat
- Gruppen-Leistung
- CSV/PDF-Export

#### 6.3 Benutzerdefinierter Bereichs-Bericht (`CustomRangeReport.tsx`)
- Benutzerdefinierte Datumsbereich-Auswahl
- Anwesenheit für ausgewählten Zeitraum
- Detaillierte Analysen
- Export-Funktionalität

#### 6.4 Verspätete Ankünfte-Bericht (`LateArrivalsReport.tsx`)
- Verspätet ankommende Kinder
- Verspätungs-Muster
- Zeitanalyse
- Häufigkeits-Verfolgung

#### 6.5 Verspätete Abholungen-Bericht (`LatePickupsReport.tsx`)
- Verspätet abgeholte Kinder
- Verspätungs-Muster
- Zeitanalyse
- Eltern-Benachrichtigungs-Verfolgung

#### 6.6 Abwesenheits-Muster-Bericht (`AbsencePatternsReport.tsx`)
- Abwesenheits-Trends
- Mustererkennung
- Häufigkeits-Analyse
- Gruppen-Vergleiche

#### 6.7 Gruppen-Leistungs-Bericht (`GroupPerformanceReport.tsx`)
- Pro-Gruppe Statistiken
- Gruppen-Vergleiche
- Leistungs-Metriken
- Anwesenheitsraten

#### 6.8 Zeit-Analytik-Bericht (`TimeAnalyticsReport.tsx`)
- Zeitbasierte Analysen
- Check-in-Zeit-Verteilung
- Dauer-Analyse
- Spitzenzeit-Identifikation

**Gemeinsame Features:**
- Tab-basierter Berichts-Auswähler
- Datumsbereich-Filterung
- CSV-Export
- PDF-Export
- Druck-Funktionalität
- Berichts-Beschreibungen und Hilfetext

**API-Aufrufe:**
- Verschiedene berichtsspezifische API-Endpunkte aus `reportApi.ts`

---

### 7. Kalender & Veranstaltungen (`/admin/events`)

**Datei:** `pages/admin/Events.tsx`

**Funktionalität:**
- **Veranstaltungs-Verwaltung:**
  - Veranstaltungen mit vollständigen Details erstellen
  - Veranstaltungen bearbeiten
  - Veranstaltungen löschen
  - Veranstaltungs-Details anzeigen

- **Veranstaltungs-Informationen:**
  - Titel, Beschreibung
  - Datum und Uhrzeit
  - Ort
  - Gruppen-Zuordnungen
  - RSVP-Verfolgung

- **Ansichts-Modi:**
  - **Kalender-Ansicht:**
    - Monatliche Kalender-Anzeige
    - Veranstaltungs-Markierungen auf Daten
    - Klick zum Anzeigen von Veranstaltungs-Details
    - Navigation (vorheriger/nächster Monat)
  
  - **Tabellen-Ansicht:**
    - Liste aller Veranstaltungen
    - Sortierbare Spalten
    - Nach Datumsbereich filtern
    - Such-Funktionalität

- **RSVP-Verwaltung:**
  - RSVPs pro Veranstaltung verfolgen
  - RSVP-Statistiken
  - RSVP-Formular für Teilnehmer
  - RSVP-Status-Indikatoren

- **Erzieher-Sitzungen (Arbeitszeiten):**
  - Erzieher-Arbeits-Sitzungen erstellen
  - Arbeitszeiten verfolgen
  - Sitzungs-Verwaltung
  - Sitzungen nach CSV/Excel exportieren

- **Export-Funktionen:**
  - Veranstaltungen nach iCal-Format exportieren
  - Veranstaltungen nach CSV exportieren
  - Kalender-Ansicht exportieren
  - Sitzungen exportieren

- **Veranstaltungs-Features:**
  - Gruppen-basierte Veranstaltungen
  - Wiederkehrende Veranstaltungen-Unterstützung
  - Veranstaltungs-Erinnerungen
  - Veranstaltungs-Benachrichtigungen

**API-Aufrufe:**
- `fetchEvents()` - Veranstaltungen auflisten
- `createEvent()` - Veranstaltung erstellen
- `updateEvent()` - Veranstaltung aktualisieren
- `deleteEvent()` - Veranstaltung löschen
- `rsvpToEvent()` - RSVP zu Veranstaltung
- `fetchEventRsvpStats()` - RSVP-Statistiken abrufen
- `exportEvent()` - Veranstaltungs-Daten exportieren
- `exportEventCalendar()` - Als Kalender exportieren
- `fetchSessions()` - Erzieher-Sitzungen abrufen
- `createSession()` - Sitzung erstellen
- `updateSession()` - Sitzung aktualisieren
- `deleteSession()` - Sitzung löschen
- `exportSessions()` - Sitzungen exportieren

---

### 8. Kommunikation (`/admin/communications`)

**Datei:** `pages/admin/Communications.tsx`

**Tab-basierte Benutzeroberfläche mit 3 Tabs:**

#### 8.1 Umfragen-Tab (`SurveysTab.tsx`)
- **Umfragen-Verwaltung:**
  - Umfragen mit Fragen erstellen
  - Umfragen bearbeiten
  - Umfragen löschen
  - Umfrage-Ergebnisse anzeigen

- **Umfragen-Features:**
  - Mehrere Fragetypen
  - Antworten-Sammlung
  - Ergebnisse-Visualisierung
  - Umfragen-Statistiken

- **Empfänger:**
  - Gruppen auswählen
  - Einzelne Kinder/Eltern auswählen
  - Erzieher auswählen

#### 8.2 Ankündigungen-Tab (`AnnouncementsTab.tsx`)
- **Ankündigungs-Verwaltung:**
  - Ankündigungen erstellen
  - Ankündigungen bearbeiten
  - Ankündigungen löschen
  - Ankündigungen veröffentlichen

- **Ankündigungs-Features:**
  - Rich-Text-Inhalt
  - Empfänger-Auswahl (Gruppen, Kinder, Eltern)
  - Veröffentlichungs-Kontrolle
  - Lese-Verfolgung
  - Statistiken (gelesen/ungelesen)

- **Empfänger:**
  - Gruppen
  - Einzelne Kinder
  - Eltern
  - Erzieher

#### 8.3 Abwesenheit & Gesundheit-Tab (`AbsenceHealthTab.tsx`)
- **Abwesenheits-Meldungen:**
  - Eltern-Abwesenheits-Meldungen anzeigen
  - Abwesenheits-Meldungen überprüfen
  - Abwesenheits-Meldungen auflösen
  - Abwesenheits-Daten exportieren

- **Erzieher-Abwesenheiten:**
  - Erzieher-Abwesenheits-Datensätze erstellen
  - Abwesenheiten bearbeiten
  - Abwesenheiten auflösen
  - Abwesenheiten exportieren

- **Gesundheits-Warnungen:**
  - Gesundheits-Bulletins erstellen
  - Warnungen aktivieren/archivieren
  - Bestätigungs-Verfolgung
  - Gesundheits-Warnungen exportieren

**API-Aufrufe:**
- `getAllSurveys()` - Umfragen auflisten
- `createSurvey()` - Umfrage erstellen
- `updateSurvey()` - Umfrage aktualisieren
- `deleteSurvey()` - Umfrage löschen
- `fetchAnnouncements()` - Ankündigungen auflisten
- `createAnnouncement()` - Ankündigung erstellen
- `deleteAnnouncement()` - Ankündigung löschen
- `absenceHealthApi` - Abwesenheits- und Gesundheits-APIs

---

### 9. Chat (`/admin/chat`)

**Datei:** `pages/admin/Chat.tsx`

**Funktionalität:**
- Verwendet gemeinsame `SharedChat`-Komponente mit role="admin"
- Vollständige Chat-Funktionalität (siehe Gemeinsame Komponenten)

---

### 10. Einstellungen (`/admin/settings`)

**Datei:** `pages/admin/Settings.tsx`

**Funktionalität:**
- **Institutions-Einstellungen:**
  - Institutions-Name
  - Adresse
  - Kontaktinformationen
  - Öffnungszeiten (Öffnungszeit, Schließzeit)
  - Wiederholte Schließtage-Konfiguration

- **Schließtage-Verwaltung:**
  - Schließtage hinzufügen
  - Schließtage entfernen
  - Alle Schließtage anzeigen
  - Kalender-basierte Auswahl

- **Einstellungs-Tabs:**
  - **Allgemeine Einstellungen:**
    - Grundlegende Institutions-Informationen
    - Adress-Details
  
  - **Öffnungszeiten:**
    - Öffnungszeit
    - Schließzeit
    - Zeitformat-Konfiguration
  
  - **Feiertage & Schließtage:**
    - Feiertage hinzufügen
    - Benutzerdefinierte Schließtage hinzufügen
    - Schließtage entfernen
    - Kalender-Ansicht

- **Speichern & Validierung:**
  - Formular-Validierung
  - Einstellungen speichern
  - Erfolgs-/Fehler-Benachrichtigungen
  - Einstellungs-Persistenz

**API-Aufrufe:**
- `getInstitutionSettings()` - Einstellungen abrufen
- `updateInstitutionSettings()` - Einstellungen aktualisieren
- `addClosedDay()` - Schließtag hinzufügen
- `removeClosedDay()` - Schließtag entfernen

---

### 11. Berichte-Index (`/admin/reports`)

**Datei:** `pages/admin/Reports.tsx`

**Funktionalität:**
- Berichtstyp-Auswähler mit Tabs
- Navigation zu einzelnen Berichts-Seiten
- Berichts-Beschreibungen
- Schnellzugriff auf alle 8 Berichtstypen

---

## Educator Dashboard Seiten

### 1. Dashboard (`/educator/dashboard`)

**Datei:** `pages/educator/Dashboard.tsx`

**Funktionalität:**
- **Heutige Übersicht:**
  - Heutige Kinder-Anzahl
  - Eingecheckte Kinder
  - Ausstehende Check-ins (noch nicht eingecheckt)
  - Aktuelle Aktivitäts-Feed

- **Statistik-Karten:**
  - Gesamt zugewiesene Kinder
  - Heutige Check-ins
  - Ausstehende Check-ins
  - Aktuelle Aktivitäts-Anzahl

- **Schnellzugriffe:**
  - Check-in/out
  - Kinder-Ansicht
  - Notizen
  - Chat
  - Persönliche Aufgaben

- **Persönliches Notizbuch:**
  - Private Notizen für Erzieher
  - Schnellzugriff

- **Aktuelle Aktivitäten:**
  - Letzte Check-ins/outs
  - Aktuelle Updates
  - Aktivitäts-Zeitstrahl

**API-Aufrufe:**
- `fetchTodaysChildren()` - Heutige Kinder
- `fetchPendingCheckins()` - Ausstehende Check-ins
- `fetchMyGroup()` - Erzieher-Gruppe
- `fetchEducatorCheckinStats()` - Check-in-Statistiken
- `fetchRecentActivity()` - Aktuelle Aktivitäten

---

### 2. Check-in (`/educator/checkin`)

**Datei:** `pages/educator/Checkin.tsx`

**Funktionalität:**
- **Check-in/out-Operationen:**
  - Kind einchecken (CHECK_IN)
  - Kind auschecken (CHECK_OUT)
  - Manuelle Zeitkorrektur
  - Check-in-Historie pro Kind

- **Heutige Kinder-Liste:**
  - Liste zugewiesener Kinder
  - Check-in-Status-Indikatoren
  - Schnell-Check-in/out-Buttons
  - Zeit-Anzeige

- **Statistiken:**
  - Heutige Check-ins-Anzahl
  - Ausgecheckte Anzahl
  - Ausstehende Check-ins
  - Gesamtanzahl Kinder

- **Check-in-Features:**
  - Zeitkorrektur-Funktionalität
  - Check-in-Notizen/Kommentare
  - Benachrichtigungs-Versand bei Check-in
  - Check-in-Historie-Ansicht

- **Kind-Informationen:**
  - Kind-Name und Foto
  - Gruppen-Zuordnung
  - Check-in-Status
  - Letzte Check-in-Zeit

**API-Aufrufe:**
- `fetchTodaysChildren()` - Heutige Kinder
- `checkinKind()` - Check-in/out durchführen
- `fetchChildHistory()` - Check-in-Historie
- `correctCheckinTime()` - Check-in-Zeit korrigieren
- `sendNotification()` - Benachrichtigungen senden

---

### 3. Kinder-Ansicht (`/educator/kinder`)

**Datei:** `pages/educator/Kinder.tsx`

**Funktionalität:**
- **Zugewiesene Kinder-Liste:**
  - Alle zugewiesenen Kinder anzeigen
  - Kind-Details
  - Gruppen-Informationen
  - Check-in-Status

- **Kind-Informationen:**
  - Name, Foto
  - Gruppen-Zuordnung
  - Eltern-Informationen
  - Medizinische Informationen (Allergien, Bedingungen)
  - Einwilligungs-Status

- **Filterung:**
  - Nach Gruppe filtern
  - Nach Name suchen
  - Datumsbasierte Filterung

- **Schnellaktionen:**
  - Kind-Details anzeigen
  - Check-in/out
  - Notizen anzeigen
  - Chat öffnen

**API-Aufrufe:**
- `fetchMyGroup()` - Erzieher-Gruppe abrufen
- `fetchTodaysChildren()` - Kinder abrufen

---

### 4. Notizen (`/educator/notizen`)

**Datei:** `pages/educator/Notizen.tsx`

**Funktionalität:**
- **Notizen-Verwaltung:**
  - Notizen für Kinder erstellen
  - Notizen bearbeiten
  - Notizen löschen
  - Notizen massenweise löschen
  - Notiz-Details anzeigen

- **Notiz-Typen:**
  - GENERAL - Allgemeine Beobachtungen
  - BEHAVIOR - Verhaltens-Notizen
  - HEALTH - Gesundheits-bezogene Notizen
  - DEVELOPMENT - Entwicklungs-Notizen
  - INCIDENT - Vorfälle-Berichte

- **Notiz-Features:**
  - Rich-Text-Inhalt
  - Dateianhänge (Fotos, PDFs)
  - Private Notizen (nur Erzieher)
  - Notizen-Suche
  - Nach Typ, Kind, Datum filtern
  - Sortier-Optionen

- **Notiz-Anzeige:**
  - Karten-basiertes Layout
  - Notiz-Typ-Indikatoren
  - Anhang-Vorschauen
  - Zeitstempel-Anzeige
  - Kind-Informationen

- **Export:**
  - Notizen nach CSV exportieren
  - Export mit Anhängen
  - Gefilterter Export

**API-Aufrufe:**
- `getNotes()` - Alle Notizen auflisten
- `getChildNotes()` - Notizen für spezifisches Kind abrufen
- `createNote()` - Notiz erstellen
- `updateNote()` - Notiz aktualisieren
- `deleteNote()` - Notiz löschen
- `deleteMultipleNotes()` - Massenlöschung
- `exportNotes()` - Notizen exportieren
- `searchNotes()` - Notizen suchen

---

### 5. Chat (`/educator/chat`)

**Datei:** `pages/educator/Chat.tsx`

**Funktionalität:**
- Verwendet gemeinsame `SharedChat`-Komponente mit role="educator"
- Vollständige Chat-Funktionalität (siehe Gemeinsame Komponenten)

---

## Gemeinsame Komponenten

### Chat-Komponente (`SharedChat.tsx`)

**Ort:** `components/chat/SharedChat.tsx`

**Funktionalität:**
- **Echtzeit-Messaging:**
  - WebSocket-basierte Kommunikation
  - Direktnachrichten (1-zu-1)
  - Gruppen-Gespräche
  - Nachrichten-Reaktionen (Emojis)
  - Tipp-Indikatoren
  - Lesebestätigungen
  - Online-Status

- **Nachrichten-Features:**
  - Textnachrichten
  - Dateianhänge (Bilder, PDFs)
  - Nachrichten bearbeiten
  - Nachrichten löschen
  - Nachrichten-Suche
  - Nachrichten-Paginierung

- **Gesprächs-Verwaltung:**
  - Neue Gespräche erstellen
  - Gesprächs-Liste
  - Gesprächs-Einstellungen
  - Teilnehmer-Verwaltung

- **UI-Features:**
  - Vollbild-Chat-Benutzeroberfläche
  - Responsives Design
  - Dark-Mode-Unterstützung
  - Datei-Upload
  - Bildbetrachter
  - Nachrichten-Status-Indikatoren

**API-Aufrufe:**
- `conversationApi.ts` - Alle Gesprächs-APIs
- WebSocket-Service für Echtzeit-Updates

---

## API Services

Das Dashboard verwendet **29 API-Service-Dateien** in `services/`:

1. `absenceApi.ts` - Abwesenheits-Meldungen
2. `absenceHealthApi.ts` - Abwesenheiten und Gesundheits-Warnungen
3. `activityApi.ts` - Aktivitätsprotokolle
4. `adminApi.ts` - Admin-spezifische APIs
5. `announcementsApi.ts` - Ankündigungen
6. `apiClient.ts` - Basis-API-Client
7. `authApi.ts` - Authentifizierung
8. `calendarApi.ts` - Kalender und Sitzungen
9. `conversationApi.ts` - Chat-Gespräche
10. `dokugenApi.ts` - KI-Dokumentenerstellung
11. `educatorApi.ts` - Erzieher-spezifische APIs
12. `eventApi.ts` - Veranstaltungen
13. `gdprApi.ts` - GDPR-Compliance
14. `healthAlertsApi.ts` - Gesundheits-Warnungen
15. `institutionSettingsApi.ts` - Institutions-Einstellungen
16. `messagingApi.ts` - Messaging
17. `noteApi.ts` - Notizen
18. `notificationsApi.ts` - Benachrichtigungen
19. `notificationService.ts` - Benachrichtigungs-Service
20. `offlineService.ts` - Offline-Unterstützung
21. `personalTaskApi.ts` - Persönliche Aufgaben
22. `profileApi.ts` - Benutzer-Profil
23. `recipientsService.ts` - Empfänger-Verwaltung
24. `reportApi.ts` - Berichte
25. `superAdminApi.ts` - Super Admin APIs
26. `surveysApi.ts` - Umfragen
27. `traegerAdminApi.ts` - Träger Admin APIs
28. `uploadApi.ts` - Datei-Uploads
29. `websocketService.ts` - WebSocket-Service

---

## Zusammenfassung

### Seitenanzahl nach Rolle

| Rolle | Seiten | Details |
|------|-------|---------|
| **SUPER_ADMIN** | 8 | Dashboard, Träger, Institutionen, Statistiken, Berichte, Educators, Parents, GDPR |
| **TRAGER_ADMIN** | 5 | Dashboard, Einrichtungen, Statistiken, Benutzer, Einstellungen |
| **ADMIN** | 11 | Dashboard, Kinder, Gruppen, Personal, Statistiken, Berichte (8 Typen), Events, Communications, Chat, Settings |
| **EDUCATOR** | 5 | Dashboard, Checkin, Kinder, Notizen, Chat |
| **Gesamt** | **29** | |

### Wichtige Features über alle Rollen hinweg

- ✅ Rollenbasierte Zugriffskontrolle
- ✅ Echtzeit-Updates (WebSocket)
- ✅ Responsives Design
- ✅ Dark-Mode-Unterstützung
- ✅ Suche und Filterung
- ✅ Paginierung
- ✅ Export-Funktionalität (CSV, PDF)
- ✅ Datei-Uploads
- ✅ Benachrichtigungen
- ✅ Aktivitätsprotokollierung
- ✅ GDPR-Compliance-Tools

---

**Letzte Aktualisierung:** Januar 2025  
**Dokumentations-Status:** ✅ Vollständig und Akkurat
