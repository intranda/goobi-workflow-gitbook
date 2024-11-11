# Authentifizierung über die Datenbank

Bei der Datenbank-Authentifizierung werden die Benutzer komplett von Goobi workflow selbst verwaltet. Nutzername und Passwort werden in der Goobi-Datenbank gespeichert. Innerhalb der Datenbank wird von dem Passwort lediglich ein Hash (`sha256` & `salt`) gespeichert und für den Vergleich mit dem eingegebenen Nutzerpasswort beim Login verglichen.