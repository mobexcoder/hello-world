# Dynamische Gruppe in Microsoft Entra ID für Intune Autopilot

## Zweck

Diese dynamische Gruppe enthält automatisch alle Geräte aus Intune Autopilot, deren **GroupTag** entweder **"Herbolzheim"** oder **"Kenzingen"** ist.

## Gruppeneinstellungen

| Einstellung              | Wert                                                        |
|--------------------------|-------------------------------------------------------------|
| **Gruppentyp**           | Sicherheit                                                  |
| **Gruppenname**          | Autopilot – Herbolzheim und Kenzingen                       |
| **Mitgliedschaftstyp**   | Dynamisches Gerät (Dynamic Device)                          |

## Dynamische Mitgliedschaftsregel

```
(device.devicePhysicalIds -any (_ -eq "[OrderID]:Herbolzheim")) -or (device.devicePhysicalIds -any (_ -eq "[OrderID]:Kenzingen"))
```

> **Hinweis:** Der Autopilot **GroupTag** wird in Entra ID als `[OrderID]` innerhalb des Attributs `devicePhysicalIds` gespeichert.

## Anleitung: Gruppe erstellen

1. Melden Sie sich im [Microsoft Entra Admin Center](https://entra.microsoft.com) an.
2. Navigieren Sie zu **Identität** → **Gruppen** → **Alle Gruppen**.
3. Klicken Sie auf **Neue Gruppe**.
4. Wählen Sie als **Gruppentyp**: `Sicherheit`.
5. Geben Sie einen **Gruppennamen** ein, z. B. `Autopilot – Herbolzheim und Kenzingen`.
6. Wählen Sie als **Mitgliedschaftstyp**: `Dynamisches Gerät`.
7. Klicken Sie auf **Dynamische Abfrage hinzufügen**.
8. Wechseln Sie im Regeleditor in den Modus **Regelsyntax bearbeiten**.
9. Fügen Sie folgende Regel ein:
   ```
   (device.devicePhysicalIds -any (_ -eq "[OrderID]:Herbolzheim")) -or (device.devicePhysicalIds -any (_ -eq "[OrderID]:Kenzingen"))
   ```
10. Klicken Sie auf **Speichern**, um die Regel zu übernehmen.
11. Klicken Sie auf **Erstellen**, um die Gruppe anzulegen.

## Überprüfung

- Nach dem Erstellen der Gruppe kann es einige Minuten dauern, bis die Mitglieder dynamisch aufgelöst werden.
- Unter **Gruppen** → *Ihre Gruppe* → **Mitglieder** können Sie überprüfen, ob die Autopilot-Geräte korrekt zugewiesen wurden.
- Unter **Dynamische Mitgliedschaftsregeln** → **Regeln überprüfen** können Sie einzelne Geräte testen.
