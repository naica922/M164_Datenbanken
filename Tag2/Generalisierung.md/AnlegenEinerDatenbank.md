# Anlegen einer Datenbank
In MySQL ist ein Schema ein Synonym für Datenbank. DBS können mehrere Schemas haben. 

## Definition Character Set
- ASCII
7-Bit-Code mit 32 Steuerzeichen und 96 druckbaren Zeichen, auf Englisch ausgerichtet.

- ANSI
SO-8859-1 (Latin1) für Westeuropa, deckt fast alle ASCII-Zeichen ab und codiert zusätzliche internationale Zeichen.

- Unicode
Umfassendster Zeichensatz, der alle Sprachen der Welt unterstützt, mit bis zu 100.000 verschiedenen Zeichen.

- UTF-8
Häufigste Unicode-Kodierung mit variabler Zeichenlänge (1 bis 4 Bytes), wobei die ersten 128 Zeichen mit ASCII identisch sind.

- UTF-16, UTF-32
UTF-16 verwendet 16-Bit-Zeichen (Java), UTF-32 hat eine fixe Zeichenlänge von 32 Bit, was zu hohem Speicherbedarf für ASCII-Zeichen führt.

## Auftrag (Repetition)
CREATE SCHEMA/TABLE (name) -> erstellt tabelle 
CREATE SCHEMA IF NOT EXISTS `M106` DEFAULT CHARACTER SET utf8mb4;
USE `M106`;

CREATE TABLE IF NOT EXISTS `tbl_fahrer` (
  `Fahrer_ID` INT NOT NULL AUTO_INCREMENT,
  `Name` VARCHAR(50) NOT NULL,
  `Vorname` VARCHAR(30) NOT NULL,
  `Geburtsdatum` DATETIME NOT NULL,
  `Telefonnummer` VARCHAR(12) NOT NULL,
  PRIMARY KEY (`Fahrer_ID`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

CREATE TABLE IF NOT EXISTS `tbl_disponent` (
  `Disponent_ID` INT NOT NULL AUTO_INCREMENT,
  `Name` VARCHAR(50) NOT NULL,
  `Vorname` VARCHAR(30) NOT NULL,
  `Geburtsdatum` DATETIME NOT NULL,
  `Telefonnummer` VARCHAR(12) NOT NULL,
  PRIMARY KEY (`Disponent_ID`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

DROP TABLE (name) -> löscht Tabelle
-- Löschen der Tabelle `tbl_fahrer`
DROP TABLE IF EXISTS `tbl_fahrer`;

-- Wiederherstellen der Tabelle `tbl_fahrer`
CREATE TABLE IF NOT EXISTS `tbl_fahrer` (
  `Fahrer_ID` INT NOT NULL AUTO_INCREMENT,
  `Name` VARCHAR(50) NOT NULL,
  `Vorname` VARCHAR(30) NOT NULL,
  `Geburtsdatum` DATETIME NOT NULL,
  `Telefonnummer` VARCHAR(12) NOT NULL,
  PRIMARY KEY (`Fahrer_ID`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

ALTER TABLE (name) MODIFY/CHANGE -> Änderungen vornehmen
CREATE TABLE IF NOT EXISTS `tbl_Mitarbeiter` (
  `MA_ID` INT NOT NULL AUTO_INCREMENT,
  `Name` VARCHAR(50) NOT NULL,
  `Vorname` VARCHAR(30) NOT NULL,
  `Geburtsdatum` DATETIME NOT NULL,
  `Telefonnummer` VARCHAR(12) NOT NULL,
  `Einkommen` FLOAT(10,2) NOT NULL,
  PRIMARY KEY (`MA_ID`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;


ALTER TABLE `tbl_Mitarbeiter`
  MODIFY `Name` VARCHAR(50) CHARACTER SET latin1,
  MODIFY `Vorname` VARCHAR(30) CHARACTER SET latin1;

ALTER TABLE DROP COLUMN (name) -> Attribute etc löschen
ALTER TABLE `tbl_fahrer`
  DROP COLUMN `Name`,
  DROP COLUMN `Vorname`,
  DROP COLUMN `Telefonnummer`;

ALTER TABLE `tbl_disponent`
  DROP COLUMN `Name`,
  DROP COLUMN `Vorname`,
  DROP COLUMN `Telefonnummer`;

ALTER TABLE ADD COLUMN -> Spezialisieren 
ALTER TABLE `tbl_fahrer`
  ADD COLUMN `MA_ID` INT NOT NULL,
  ADD CONSTRAINT `fk_fahrer_mitarbeiter`
  FOREIGN KEY (`MA_ID`) REFERENCES `tbl_Mitarbeiter`(`MA_ID`);

ALTER TABLE `tbl_disponent`
  ADD COLUMN `MA_ID` INT NOT NULL,
  ADD CONSTRAINT `fk_disponent_mitarbeiter`
  FOREIGN KEY (`MA_ID`) REFERENCES `tbl_Mitarbeiter`(`MA_ID`);



## Forward Engineering mit Workbench 
-- MySQL Workbench Forward Engineering

SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION';

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------
DROP SCHEMA IF EXISTS `mydb` ;

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------
CREATE SCHEMA IF NOT EXISTS `mydb` DEFAULT CHARACTER SET utf8 ;
USE `mydb` ;

-- -----------------------------------------------------
-- Table `Person`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `Person` ;

CREATE TABLE IF NOT EXISTS `Person` (
  `Name` INT NOT NULL,
  `Name` VARCHAR(45) NULL,
  `Vorname` VARCHAR(45) NULL,
  `Grösse` DECIMAL NULL,
  PRIMARY KEY (`Name`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `Kleidungsstück_NI`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `Kleidungsstück_NI` ;

CREATE TABLE IF NOT EXISTS `Kleidungsstück_NI` (
  `idKleidungsstück_NI` INT NOT NULL,
  `Bezeichnung` VARCHAR(45) NULL,
  `Grösse` VARCHAR(45) NULL,
  `Farbe` VARCHAR(45) NULL,
  `Person_Name` INT NOT NULL,
  PRIMARY KEY (`idKleidungsstück_NI`),
  INDEX `fk_Kleidungsstück_NI_Person_idx` (`Person_Name` ASC) VISIBLE,
  CONSTRAINT `fk_Kleidungsstück_NI_Person`
    FOREIGN KEY (`Person_Name`)
    REFERENCES `Person` (`Name`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `Ausweis_I`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `Ausweis_I` ;

CREATE TABLE IF NOT EXISTS `Ausweis_I` (
  `PS_Ausweis_ID` INT NOT NULL,
  `Bezeichnung` VARCHAR(45) NULL,
  `Ausstellungsdatum` DATETIME NULL,
  `Nummer` VARCHAR(45) NULL,
  `Person_Name` INT NOT NULL,
  PRIMARY KEY (`PS_Ausweis_ID`, `Person_Name`),
  INDEX `fk_Ausweis_I_Person1_idx` (`Person_Name` ASC) VISIBLE,
  CONSTRAINT `fk_Ausweis_I_Person1`
    FOREIGN KEY (`Person_Name`)
    REFERENCES `Person` (`Name`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;

-- MySQL Workbench Forward Engineering

SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION';

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------
-- -----------------------------------------------------
-- Schema new_schema
-- -----------------------------------------------------
DROP SCHEMA IF EXISTS `new_schema` ;

-- -----------------------------------------------------
-- Schema new_schema
-- -----------------------------------------------------
CREATE SCHEMA IF NOT EXISTS `new_schema` DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci ;
USE `new_schema` ;

-- -----------------------------------------------------
-- Table `disponenten`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `disponenten` ;

CREATE TABLE IF NOT EXISTS `disponenten` (
  `Disponent_ID` INT NOT NULL AUTO_INCREMENT,
  `Name` VARCHAR(255) NULL DEFAULT NULL,
  `Telefonnummer` VARCHAR(20) NULL DEFAULT NULL,
  PRIMARY KEY (`Disponent_ID`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `fahrer`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `fahrer` ;

CREATE TABLE IF NOT EXISTS `fahrer` (
  `Fahrer_ID` INT NOT NULL AUTO_INCREMENT,
  `Name` VARCHAR(255) NULL DEFAULT NULL,
  `Telefonnummer` VARCHAR(20) NULL DEFAULT NULL,
  PRIMARY KEY (`Fahrer_ID`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `fahrzeuge`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `fahrzeuge` ;

CREATE TABLE IF NOT EXISTS `fahrzeuge` (
  `Fahrzeug_ID` INT NOT NULL AUTO_INCREMENT,
  `Sitzplatzanzahl` INT NULL DEFAULT NULL,
  PRIMARY KEY (`Fahrzeug_ID`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `fahrten`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `fahrten` ;

CREATE TABLE IF NOT EXISTS `fahrten` (
  `Fahrt_ID` INT NOT NULL AUTO_INCREMENT,
  `Disponent_ID` INT NULL DEFAULT NULL,
  `Fahrzeug_ID` INT NULL DEFAULT NULL,
  PRIMARY KEY (`Fahrt_ID`),
  INDEX `Disponent_ID` (`Disponent_ID` ASC) VISIBLE,
  INDEX `Fahrzeug_ID` (`Fahrzeug_ID` ASC) VISIBLE,
  CONSTRAINT `fahrten_ibfk_1`
    FOREIGN KEY (`Disponent_ID`)
    REFERENCES `disponenten` (`Disponent_ID`),
  CONSTRAINT `fahrten_ibfk_2`
    FOREIGN KEY (`Fahrzeug_ID`)
    REFERENCES `fahrzeuge` (`Fahrzeug_ID`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `fahrten_fahrer`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `fahrten_fahrer` ;

CREATE TABLE IF NOT EXISTS `fahrten_fahrer` (
  `Fahrt_ID` INT NOT NULL,
  `Fahrer_ID` INT NOT NULL,
  PRIMARY KEY (`Fahrt_ID`, `Fahrer_ID`),
  INDEX `Fahrer_ID` (`Fahrer_ID` ASC) VISIBLE,
  CONSTRAINT `fahrten_fahrer_ibfk_1`
    FOREIGN KEY (`Fahrt_ID`)
    REFERENCES `fahrten` (`Fahrt_ID`),
  CONSTRAINT `fahrten_fahrer_ibfk_2`
    FOREIGN KEY (`Fahrer_ID`)
    REFERENCES `fahrer` (`Fahrer_ID`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `tbl_mitarbeiter`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `tbl_mitarbeiter` ;

CREATE TABLE IF NOT EXISTS `tbl_mitarbeiter` (
  `MA_ID` INT NOT NULL,
  `Name` VARCHAR(50) CHARACTER SET 'latin1' NULL DEFAULT NULL,
  `Vorname` VARCHAR(30) CHARACTER SET 'latin1' NULL DEFAULT NULL,
  `Geburtsdatum` DATETIME NULL DEFAULT NULL,
  `Telefonnummer` VARCHAR(12) NULL DEFAULT NULL,
  `Einkommen` FLOAT(10,2) NULL DEFAULT NULL,
  `fahrer_Fahrer_ID` INT NOT NULL,
  `disponenten_Disponent_ID` INT NOT NULL,
  PRIMARY KEY (`MA_ID`),
  INDEX `fk_tbl_mitarbeiter_fahrer1_idx` (`fahrer_Fahrer_ID` ASC) VISIBLE,
  INDEX `fk_tbl_mitarbeiter_disponenten1_idx` (`disponenten_Disponent_ID` ASC) VISIBLE,
  CONSTRAINT `fk_tbl_mitarbeiter_fahrer1`
    FOREIGN KEY (`fahrer_Fahrer_ID`)
    REFERENCES `fahrer` (`Fahrer_ID`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_tbl_mitarbeiter_disponenten1`
    FOREIGN KEY (`disponenten_Disponent_ID`)
    REFERENCES `disponenten` (`Disponent_ID`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `person`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `person` ;

CREATE TABLE IF NOT EXISTS `person` (
  `PersonId` INT NOT NULL,
  `Name` VARCHAR(50) NULL DEFAULT NULL,
  `Vorname` VARCHAR(50) NULL DEFAULT NULL,
  `Gerburtsdatum` DATETIME NULL DEFAULT NULL,
  `Gewicht` MEDIUMINT NULL DEFAULT NULL,
  `Einkommen` FLOAT(10,2) NULL DEFAULT NULL,
  `tbl_mitarbeiter_MA_ID` INT NOT NULL,
  PRIMARY KEY (`PersonId`),
  INDEX `fk_person_tbl_mitarbeiter1_idx` (`tbl_mitarbeiter_MA_ID` ASC) VISIBLE,
  CONSTRAINT `fk_person_tbl_mitarbeiter1`
    FOREIGN KEY (`tbl_mitarbeiter_MA_ID`)
    REFERENCES `tbl_mitarbeiter` (`MA_ID`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `stationen`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `stationen` ;

CREATE TABLE IF NOT EXISTS `stationen` (
  `Station_ID` INT NOT NULL AUTO_INCREMENT,
  `Fahrt_ID` INT NULL DEFAULT NULL,
  `Ankunftszeit` DATETIME NULL DEFAULT NULL,
  `Abfahrtszeit` DATETIME NULL DEFAULT NULL,
  PRIMARY KEY (`Station_ID`),
  INDEX `Fahrt_ID` (`Fahrt_ID` ASC) VISIBLE,
  CONSTRAINT `stationen_ibfk_1`
    FOREIGN KEY (`Fahrt_ID`)
    REFERENCES `fahrten` (`Fahrt_ID`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;

CREATE database if not exists Kleidungsstücke;

-- Tabelle für Personen
CREATE TABLE Personen (
    Person_ID INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(50),
    Vorname VARCHAR(30),
    Geburtsdatum DATE
);

-- Tabelle für Kleidungsstücke
CREATE TABLE Kleidungsstuecke (
    Kleidungsstueck_ID INT AUTO_INCREMENT PRIMARY KEY,
    Typ VARCHAR(50),
    Groesse VARCHAR(10)
);

-- Tabelle für Ausweise
CREATE TABLE Ausweise (
    Ausweis_ID INT AUTO_INCREMENT PRIMARY KEY,
    Person_ID INT,
    Ausweisnummer VARCHAR(20),
    FOREIGN KEY (Person_ID) REFERENCES Personen(Person_ID)
);


## Recherche und Zusammenfassung
Recherchieren Sie folgende Begriffe im Internet und erstellen Sie eine Zusammenfassung ins Lernportfolio.

Tablespace, Tablespace Architecture:
Ein Tablespace ist ein logischer Speicherbereich innerhalb einer Datenbank, der verwendet wird, um Datenbankobjekte wie Tabellen und Indizes zu speichern. Ein Tablespace kann mehrere Datenbankdateien umfassen, die physisch auf verschiedenen Speichergeräten gespeichert sind.
Tablespace Architecture:
Die Architektur eines Tablespace umfasst mehrere Komponenten:
Datenbankdateien: Physische Dateien auf dem Speichergerät, in denen die Daten gespeichert werden.
Segments: Logische Einheiten innerhalb eines Tablespace, die Tabellen, Indizes oder andere Datenbankobjekte enthalten.
Extents: Gruppen von zusammenhängenden Datenblöcken, die von einem Segment verwendet werden.
Datenblöcke: Die kleinste Speichereinheit innerhalb eines Tablespace, die tatsächliche Daten enthält.
Diese Struktur virtueller Speicher (cache) ermöglicht eine effiziente Verwaltung und Zuweisung von Speicherplatz innerhalb der Datenbank.

Partition (bezgl. Datenbanken):
Partitionierung in Datenbanken bezieht sich auf das Aufteilen großer Tabellen in kleinere, besser verwaltbare Teile, die als Partitionen bezeichnet werden. Jede Partition kann unabhängig verwaltet, indiziert und abgefragt werden. Dies verbessert die Leistung und die Verwaltungsfähigkeiten der Datenbank.
Partitionen können basierend auf verschiedenen Kriterien erstellt werden, darunter:
Bereichspartitionierung (Range Partitioning): Aufteilung basierend auf einem Bereich von Werten, z.B. Datumswerte.
Listenpartitionierung (List Partitioning): Aufteilung basierend auf einer vordefinierten Liste von Werten.
Hash-Partitionierung (Hash Partitioning): Aufteilung basierend auf einem Hash-Wert einer Spalte.
Schlüsselpartitionierung (Key Partitioning): Aufteilung basierend auf einem Primär- oder Fremdschlüssel.
Die Partitionierung erleichtert das Laden und Verwalten großer Datenmengen und verbessert die Abfrageleistung, indem nur relevante Partitionen durchsucht werden.

Was macht eine storage engine in einer Datenbank?:
Eine Storage Engine ist die Komponente einer Datenbank, die für das Speichern, Abrufen und Verwalten von Daten verantwortlich ist. Sie definiert, wie Daten auf physischer Ebene gespeichert werden und welche Operationen unterstützt werden. Verschiedene Storage Engines bieten unterschiedliche Funktionen und Optimierungen.
Beispiele für Storage Engines:
InnoDB: Bietet ACID-Konformität, Transaktionsunterstützung, Fremdschlüssel, und Row-Level-Locking. Sie ist die Standard-Storage-Engine in MySQL.
MyISAM: Eine ältere Storage Engine, die keine Transaktionen unterstützt, aber für schnelle Leseoperationen optimiert ist.
Memory: Speichert Daten im RAM für schnelle Zugriffe, eignet sich für temporäre Daten oder Caching.
CSV: Speichert Daten im CSV-Format, was den Datenaustausch zwischen verschiedenen Systemen erleichtert.
Jede Storage Engine hat spezifische Anwendungsfälle und Performance-Eigenschaften, die je nach den Anforderungen der Anwendung ausgewählt werden können.
