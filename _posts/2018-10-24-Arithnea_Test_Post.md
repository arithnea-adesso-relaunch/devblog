---
layout:         [post, post-xml]              
title:          "Dies ist ein Test Blog Post um den Import ins FS System zu testen"
date:           2018-10-24 11:01
modified_date: 
author:         arithnea
categories:     [Java, Architektur]
tags:           [Spring, Microservices]
---

Aufgrund von mehreren Tickets, in denen es um das Importieren der GitHub Blog-Posts nach FirstSpirit geht, werden wir den Importer 
noch einmal grundlegend testen. Dafür ist dieser Testbeitrag gedacht.

# Der Auftrag Import Github Blog Posts
> Da Datensätze innerhalb von FS geändert werden, ist eine *eigene* Verbindung notwendig!
Der Schritt [Copy Only] Import Github Blog führt in einem Modul folgende Schritte aus:
* Clonen des Repositories / Wenn bereits vorhanden, pullen des neuesten Standes von repositoryUrl in das Vereichnis repositoryPath
> Der Pfad repositoryPath muss existieren und für den *fs5* Nutzer schreibbar sein.
* Parsen der XML-Dateien in dem Verzeichnis importPath
* Konvertierung des XMLs zu einem FirstSpirit Datensatz. Hierfür wird die Datenquelle blogContent2Name sowie categoriesContent2Name verwendet.
> Zusätzlich werden Tags in eine fest definierte Datenquelle tags importiert. Autoren werden mit der Datenquelle autoren abgeglichen. TODO: als Parameter übergeben
* Alle importierten Datensätze werden automatisch freigegeben

> Datensätze werden bei jedem durchlaufen *nicht* neu importiert. Hierfür wird eine Prüfsumme über den Inhalt gebildet, die beim Import abgeglichen wird (zu finden im Feld tt_checksum). Zusätzlich wird das Feld tt_github_last_change mit dem letzten Änderungsdatum aus dem XML gefüllt.
