# App4KITAs Dashboard - Vollständige Funktionalitäts-Dokumentation

**Letzte Aktualisierung: Oktober 2025**  

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
- **Plattform-Statistiken (4 StatCards):**
  - Gesamt Nutzer (users)
  - Institutionen (institutionen)
  - Aktive Nutzer (activeUsers)
  - Inaktive Nutzer (inactiveUsers)

- **Schnellzugriffe (4 Action Buttons):**
  - Institutionen verwalten → `/dashboard/superadmin/institutionen`
  - Nutzer verwalten → `/dashboard/superadmin/erzieher`
  - Statistiken anzeigen → `/dashboard/superadmin/statistiken`
  - DSGVO Compliance → `/dashboard/superadmin/gdpr`

- **Persönliches Notizbuch:**
  - PersonalNotebook Komponente (volle Breite)

- **Aktivitätsprotokoll:**
  - ActivityLog Komponente (letzte 10 Aktivitäten)

**API-Aufrufe:**
- `getSuperAdminStats()` - Plattform-Statistiken (users, institutionen, activity, activeUsers, inactiveUsers, children, checkInsToday, trends)

---

### 2. Träger-Verwaltung (`/super-admin/traeger`)

**Datei:** `pages/super_admin/Traeger.tsx`

**Funktionalität:**
- **Zwei separate CRUD-Bereiche:**

  **1. Träger Übersicht:**
  - Träger erstellen (Name*, Adresse, Kontakt E-Mail, Kontakt Telefon)
  - Träger bearbeiten
  - Träger löschen
  - Spalten: Name, Adresse, Kontakt E-Mail, Kontakt Telefon, Einrichtungen (Anzahl), Erstellt von
  - Suche, Paginierung

  **2. Träger-Admin Übersicht:**
  - Träger-Admin erstellen (Name*, E-Mail*, Passwort*, Träger*)
  - Träger-Admin bearbeiten (Name, E-Mail, optionales neues Passwort)
  - Träger-Admin löschen
  - Spalten: Träger-Admin (Name mit Avatar), Kontakt (E-Mail + Träger-Name), Status (klickbarer Badge + Letzter Login)
  - Status-Badge: Aktiv/Inaktiv/Gesperrt (klickbar zum Umschalten)
  - Suche, Paginierung

- **Validierung:**
  - E-Mail-Format-Prüfung
  - Duplikat-Prüfung (E-Mail bereits vergeben)
  - Träger-Name-Eindeutigkeit

**API-Aufrufe:**
- `getAllTraeger()` - Alle Träger auflisten
- `createTraeger()` - Träger erstellen
- `updateTraeger()` - Träger aktualisieren
- `deleteTraeger()` - Träger löschen
- `getAllTraegerAdmins()` - Alle Träger-Admins auflisten
- `createTraegerAdmin()` - Träger-Admin erstellen
- `updateTraegerAdmin()` - Träger-Admin aktualisieren
- `deleteTraegerAdmin()` - Träger-Admin löschen
- `fetchAllUsers()` - Alle Benutzer abrufen (für Duplikat-Prüfung)
- `updateUserStatus()` - Benutzerstatus aktualisieren (Toggle)

---

### 3. Institutionen (`/super-admin/institutionen`)

**Datei:** `pages/super_admin/Institutionen.tsx`

**Funktionalität:**
- **Zwei separate CRUD-Bereiche:**

  **1. Institutionen Übersicht:**
  - Institution erstellen (Name*, Adresse*, Träger*)
  - Institution bearbeiten (Name, Adresse, Träger)
  - Institution löschen
  - Spalten: Name, Adresse, Träger
  - Suche, Paginierung

  **2. Kitaleitung Übersicht:**
  - Kitaleitung (Admin) erstellen (Name*, E-Mail*, Passwort*, Institution*)
  - Kitaleitung bearbeiten (Name, E-Mail, optionales neues Passwort)
  - Kitaleitung löschen
  - Spalten: Kitaleitung (Name mit Avatar), Kontakt (E-Mail + Institution-Name), Status (klickbarer Badge + Letzter Login)
  - Status-Badge: Aktiv/Inaktiv/Gesperrt (klickbar zum Umschalten)
  - Suche, Paginierung

- **Validierung:**
  - E-Mail-Format-Prüfung
  - Duplikat-Prüfung (E-Mail bereits vergeben)
  - Institution-Name-Eindeutigkeit

**API-Aufrufe:**
- `fetchInstitutionen()` - Alle Institutionen auflisten
- `addKita()` - Institution erstellen
- `editKita()` - Institution aktualisieren
- `deleteKita()` - Institution löschen
- `fetchInstitutionenAdmins()` - Alle Admins auflisten
- `registerAdmin()` - Admin erstellen
- `editAdmin()` - Admin aktualisieren
- `deleteAdmin()` - Admin löschen
- `getAllTraeger()` - Träger für Dropdown
- `fetchAllUsers()` - Alle Benutzer abrufen (für Duplikat-Prüfung)
- `updateUserStatus()` - Benutzerstatus aktualisieren (Toggle)

---

### 4. Statistiken (`/super-admin/statistiken`)

**Datei:** `pages/super_admin/Statistiken.tsx`

**Funktionalität:**
- **Zeitraum-Auswahl:**
  - 7 Tage, 30 Tage, 90 Tage, 1 Jahr
  - Aktualisieren-Button
  - Auto-Refresh alle 5 Minuten

- **Export-Funktionen:**
  - Excel-Export (`.xlsx`)
  - PDF-Export (`.pdf`)

- **Statistik-Kategorien (7 Sektionen):**

  **1. Key Performance Indicators:**
  - Gesamt Nutzer, Aktive Nutzer, Institutionen, Kinder

  **2. Nutzer & Engagement:**
  - Admins, Erzieher:innen, Eltern, Gruppen

  **3. Aktivität & Check-ins:**
  - Gesamt Check-ins, Heutige Check-ins, Verspätete Check-ins, Ø Check-ins/Kind

  **4. Kommunikation:**
  - Gesamt Nachrichten, Nachrichten (Zeitraum), Gesamt Benachrichtigungen, Ø Nachrichten/Nutzer

  **5. Aufgaben & Produktivität:**
  - Gesamt Aufgaben, Abgeschlossene Aufgaben, Ausstehende Aufgaben, Erfolgsrate

  **6. Inhalte & Veranstaltungen:**
  - Veranstaltungen, Ankündigungen, Umfragen, Aktivitäts-Logs

  **7. Sicherheit & Compliance:**
  - Fehlgeschlagene Logins, Einverständniserklärungen, DSGVO-Anfragen

- **StatCard Features:**
  - Trend-Indikatoren (↑/↓ mit Prozent)
  - Icons, Beschreibungen
  - Hover-Effekte

**API-Aufrufe:**
- `getSuperAdminStats(period)` - Plattform-Statistiken mit Zeitraum
- `/api/reports/platform-stats?format=excel&period={period}` - Excel-Export
- `/api/reports/platform-stats?format=pdf&period={period}` - PDF-Export

---

### 5. Berichte (`/super-admin/reports`)

**Datei:** `pages/super_admin/Reports.tsx`

**Funktionalität:**
- **9 Report-Karten in 2 Sektionen:**

  **Sektion 1: Nutzer & Aktivität (6 Reports):**
  1. **Benutzerwachstum** - Datumsbereich (Von/Bis), Presets: Dieses Jahr / Letzte 30 Tage / Letzte 7 Tage
  2. **Aktive Nutzer** - Tage (1-365), Presets: 7/30/90 Tage
  3. **Check-in Trends** - Datumsbereich (Von/Bis), Presets
  4. **Aktive Gruppen** - Datumsbereich (Von/Bis), Presets
  5. **Nachrichtenvolumen** - Datumsbereich (Von/Bis), Presets
  6. **Benachrichtigungsstatistiken** - Datumsbereich (Von/Bis), Presets

  **Sektion 2: Sicherheit & Qualität (3 Reports):**
  7. **Fehlgeschlagene Logins** - Datumsbereich (Von/Bis), Presets
  8. **Gruppenanwesenheit** - Datumsbereich (Von/Bis), Presets
  9. **Check-in Methoden** - Datumsbereich (Von/Bis), Presets

- **Jede Report-Karte:**
  - Icon, Titel mit Tooltip, Untertitel
  - Preset-Buttons (Dieses Jahr / Letzte 30 Tage / Letzte 7 Tage)
  - Datumsbereich-Eingabe (Von/Bis) oder Tage-Eingabe
  - Validierung (Enddatum nicht vor Startdatum)
  - PDF Export-Button
  - Excel Export-Button

**API-Aufrufe:**
- `handleExport()` aus `reportApi.ts` für alle Exporte
- Endpunkte: `/reports/user-growth`, `/reports/active-users`, `/reports/checkin-trends`, `/reports/active-groups`, `/reports/message-volume`, `/reports/notification-stats`, `/reports/failed-logins`, `/reports/group-attendance`, `/reports/checkin-methods`

---

### 6. Erzieher (`/super-admin/educators`)

**Datei:** `pages/super_admin/Educators.tsx`

**Funktionalität:**
- **Erzieher CRUD:**
  - Erzieher erstellen (Name*, E-Mail*, Passwort*, Institution*, Gruppen (mehrfach), Status, Push-Token)
  - Erzieher bearbeiten (Name, E-Mail, optionales neues Passwort, Institution, Gruppen, Status, Push-Token)
  - Erzieher löschen

- **Spalten:**
  - Erzieher: Name, E-Mail, Institution-Name
  - Status: Klickbarer Badge (Aktiv/Inaktiv/Gesperrt) + Letzter Login

- **Formular-Features:**
  - SearchableDropdown für Institution (erforderlich)
  - SearchableDropdown für Gruppen (mehrfach auswählbar)
  - Status-Auswahl (Aktiv/Inaktiv)
  - Push-Token (optional, für mobile Benachrichtigungen)

- **Validierung:**
  - E-Mail-Format-Prüfung
  - Duplikat-Prüfung (E-Mail bereits vergeben)

- **Suche & Paginierung**

**API-Aufrufe:**
- `fetchEducators()` - Alle Erzieher auflisten
- `addEducator()` - Erzieher erstellen
- `editEducator()` - Erzieher aktualisieren
- `deleteEducator()` - Erzieher löschen
- `fetchInstitutionen()` - Institutionen für Dropdown
- `fetchGroups()` - Gruppen für Dropdown
- `fetchAllUsers()` - Alle Benutzer (für Duplikat-Prüfung)
- `updateUserStatus()` - Status-Toggle

---

### 7. Eltern (`/super-admin/parents`)

**Datei:** `pages/super_admin/Parents.tsx`

**Funktionalität:**
- **Eltern CRUD:**
  - Elternteil erstellen (Name*, E-Mail*, Passwort*, Telefon, Status, Push-Token)
  - Elternteil bearbeiten (Name, E-Mail, optionales neues Passwort, Telefon, Status, Push-Token)
  - Elternteil löschen

- **Spalten:**
  - Elternteil: Name, E-Mail, Telefon (falls vorhanden)
  - Status: Klickbarer Badge (Aktiv/Inaktiv/Gesperrt) + Letzter Login

- **Formular-Features:**
  - Status-Auswahl (Aktiv/Inaktiv)
  - Push-Token (optional, für mobile Benachrichtigungen)
  - Einzelnes Modal für Erstellen/Bearbeiten (unterscheidet anhand von editId)

- **Validierung:**
  - E-Mail-Format-Prüfung
  - Duplikat-Prüfung (E-Mail bereits vergeben)

- **Suche & Paginierung**

**API-Aufrufe:**
- `fetchParents()` - Alle Eltern auflisten
- `addParent()` - Elternteil erstellen
- `editParent()` - Elternteil aktualisieren
- `deleteParent()` - Elternteil löschen
- `fetchAllUsers()` - Alle Benutzer (für Duplikat-Prüfung)
- `updateUserStatus()` - Status-Toggle

---

### 8. GDPR-Compliance (`/super-admin/gdpr`)

**Datei:** `pages/super_admin/GDPRCompliancePage.tsx`

**Funktionalität:**
- **9 Tabs mit umfassender GDPR-Funktionalität:**

  **1. Audit-Logs:**
  - Filter: Von Datum, Bis Datum, Aktion, Benutzer
  - Tabelle: Datum, Aktion, Benutzer, Details
  - Paginierung (10 Einträge pro Seite)
  - Formatierte Anzeige (relative Zeit, Icons, Status-Badges)

  **2. Löschungsanfragen:**
  - Tabelle: Benutzer, Grund, Status, Erstellt am, Aktionen
  - Genehmigen/Ablehnen-Buttons für PENDING-Status

  **3. Ausstehende Löschungen:**
  - Tabelle: Typ, Name, Institution, Löschung am, Permanente Löschung, Status
  - Status-Badges (Kritisch/Warnung/Normal) basierend auf Tagen bis permanenter Löschung

  **4. Datenexport:**
  - Formular: User-ID eingeben
  - JSON-Export-Download

  **5. Bereinigung:**
  - Formular: Monate zurück (1-60)
  - Manuelle Bereinigung starten
  - Ergebnis-Anzeige

  **6. Compliance-Reports:**
  - Compliance Score (0-100) mit visueller Anzeige
  - Statistiken: Datenverarbeitung, Datenlöschung, Datenexport, Datenschutzbeschwerden
  - Compliance-Empfehlungen mit Priorität (HIGH/MEDIUM/LOW)

  **7. Backup-Verifizierung:**
  - Backup-Status-Anzeige
  - Verifizierungsergebnisse nach Typ
  - Manuelle Verifizierung starten

  **8. Privacy-by-Design:**
  - Implementierungs-Button
  - Status-Anzeige
  - Liste der implementierten Maßnahmen

  **9. Echtzeit-Monitoring:**
  - Monitoring-Status (letzte Stunde)
  - Statistiken: Verarbeitungsaktivitäten, Löschaktivitäten, Datenschutzbeschwerden
  - Alerts mit Severity (HIGH/MEDIUM/LOW)
  - Erkannte Anomalien

**API-Aufrufe:**
- `getPendingDeletions()` - Ausstehende Löschungen
- `getGDPRAuditLogs(100)` - Audit-Logs
- `getRetentionPeriods()` - Aufbewahrungsfristen
- `triggerCleanup()` - Bereinigung starten
- `generateComplianceReport()` - Compliance-Report generieren
- `verifyBackupIntegrity()` - Backup verifizieren
- `implementPrivacyByDesign()` - Privacy-by-Design implementieren
- `monitorComplianceRealTime()` - Echtzeit-Monitoring
- `getAnomalyDetection()` - Anomalien erkennen
- `getComplianceRecommendations()` - Empfehlungen abrufen
- `/api/gdpr/export/{identifier}` - Datenexport
- `/api/gdpr/requests/{id}/approve` - Anfrage genehmigen
- `/api/gdpr/requests/{id}/reject` - Anfrage ablehnen

---

## Träger Admin Dashboard Seiten

### 1. Dashboard (`/traeger-admin/dashboard`)

**Datei:** `pages/traeger_admin/Dashboard.tsx`

**Funktionalität:**
- **Träger-Statistiken (4 StatCards):**
  - Kinder gesamt (totalChildren)
  - Einrichtungen (totalInstitutions)
  - Erzieher gesamt (totalEducators)
  - Kinder >8h (childrenOver8h)

- **Warnungen (AlertCards):**
  - Inaktive Benutzer: Zeigt Anzahl inaktiver Benutzer (letzte 4 Wochen), Button → `/traegeradmin/benutzer?filter=inactive`
  - Fehlgeschlagene Logins: Zeigt Anzahl fehlgeschlagener Logins (letzte 30 Tage), Button → `/traegeradmin/statistiken`

- **Schnellzugriffe (3 QuickLinkCards):**
  - Einrichtungen → `/traegeradmin/einrichtungen`
  - Benutzer → `/traegeradmin/benutzer`
  - Statistiken → `/traegeradmin/statistiken`

**API-Aufrufe:**
- `getTraegerStats(traegerId)` - Träger-Statistiken
- `getInactiveUsers(traegerId, 4)` - Inaktive Benutzer (letzte 4 Wochen)
- `getFailedLogins(traegerId, 30)` - Fehlgeschlagene Logins (letzte 30 Tage)

---

### 2. Einrichtungen (`/traeger-admin/einrichtungen`)

**Datei:** `pages/traeger_admin/Einrichtungen.tsx`

**Funktionalität:**
- **Institution CRUD:**
  - Institution erstellen (Name*, Adresse*)
  - Institution bearbeiten (Name, Adresse)
  - Institution löschen (mit Bestätigung)

- **Spalten:**
  - Name, Adresse
  - Kinder (Anzahl aus `_count.children`)
  - Admins (Anzahl aus `_count.admins`)

- **Suche & Paginierung**

**API-Aufrufe:**
- `getTraegerInstitutions()` - Alle Institutionen des Trägers auflisten
- `createInstitution({ name, address })` - Institution erstellen
- `updateInstitution(id, { name, address })` - Institution aktualisieren
- Hinweis: Delete-Endpoint muss noch implementiert werden

---

### 3. Statistiken (`/traeger-admin/statistiken`)

**Datei:** `pages/traeger_admin/Statistiken.tsx`

**Funktionalität:**
- **Gesamtstatistiken (3 StatCards):**
  - Kinder: Gesamt (totalChildren), Über 8h (childrenOver8h)
  - Einrichtungen: Gesamt (totalInstitutions)
  - Erzieher: Gesamt (totalEducators)

- **Inaktive Benutzer:**
  - Liste der inaktiven Benutzer (letzte 4 Wochen)
  - Anzeige: Name, E-Mail, Rolle, Institution, Letzter Login

- **Fehlgeschlagene Logins:**
  - Liste der fehlgeschlagenen Login-Versuche (letzte 30 Tage)
  - Anzeige: E-Mail, Datum, IP-Adresse (falls verfügbar)

**API-Aufrufe:**
- `getTraegerStats(traegerId)` - Träger-Statistiken
- `getInactiveUsers(traegerId, 4)` - Inaktive Benutzer
- `getFailedLogins(traegerId, 30)` - Fehlgeschlagene Logins

---

### 4. Benutzer (`/traeger-admin/benutzer`)

**Datei:** `pages/traeger_admin/Benutzer.tsx`

**Funktionalität:**
- **Benutzer-Übersicht (nur Anzeige, kein CRUD):**
  - Alle Benutzer des Trägers anzeigen (PARENT wird herausgefiltert)
  - Spalten: Name, E-Mail, Rolle, Einrichtung, Status

- **Status-Verwaltung:**
  - Status-Badge (Aktiv/Inaktiv) - klickbar zum Umschalten
  - Bestätigungsdialog vor Status-Änderung
  - Sperren/Entsperren-Funktionalität

- **Suche & Paginierung**

**Hinweis:** 
- Eltern (PARENT) werden nicht angezeigt (können nicht vom Träger-Admin verwaltet werden)
- Keine Erstellen/Bearbeiten/Löschen-Funktionalität (nur Status-Toggle)

**API-Aufrufe:**
- `getTraegerUsers()` - Alle Benutzer des Trägers (PARENT wird gefiltert)
- `blockUser(traegerId, userId, isBlocked)` - Benutzer sperren/entsperren

---

### 5. Einstellungen (`/traeger-admin/einstellungen`)

**Datei:** `pages/traeger_admin/Einstellungen.tsx`

**Funktionalität:**
- **Platzhalter-Seite:**
  - Zeigt Meldung: "Einstellungen werden in einer zukünftigen Version verfügbar sein."
  - Keine aktuelle Funktionalität implementiert

**API-Aufrufe:**
- Keine (Platzhalter)

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

**Letzte Aktualisierung:** Oktober 2025  
**Dokumentations-Status:** ✅ Vollständig und Akkurat
