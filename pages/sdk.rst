.. title: LZMA SDK (Software Development Kit)
.. slug: sdk
.. date: 2026-02-12 18:38:46
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text

LZMA SDK (Software Development Kit)
===================================

Das **LZMA SDK** bietet eine Dokumentation, Beispiele, Headerdateien,
Bibliotheken und Werkzeuge, um Anwendungen zu entwickeln, die die
**LZMA**-Kompression verwenden.

.. table::
    :widths: 11 10 12 13 54

    +----------------------------------------------------------+---------+------------+-------------+------------------------------------------+
    | Link                                                     | Größe   | Datum      | Version     | Beschreibung                             |
    +==========================================================+=========+============+=============+==========================================+
    | `Download <https://7-zip.org/a/lzma2600.7z>`__           |  1,7 MB | 12.02.2026 | 26.00       | | LZMA SDK                               |
    +----------------------------------------------------------+---------+------------+-------------+ | C, C++, C#, Java                       |
    | `Download <https://7-zip.org/a/lzma2301.7z>`__           |   1 MB  | 20.06.2023 | 23.01       | | x86/x64/arm64-Binärdateien für Windows |
    +----------------------------------------------------------+---------+------------+-------------+------------------------------------------+
    | `Download <https://7-zip.org/a/lzma-specification.7z>`__ |  12 KB  | 14.06.2015 |             | LZMA-Spezifikation (Entwurf)             |
    +----------------------------------------------------------+---------+------------+-------------+------------------------------------------+


**Was ist neu:**

-  **26.00:** Einige kleine Korrekturen.
-  **25.01:** Der Code zur Verarbeitung symbolischer Links wurde geändert, um beim Entpacken von Archivdateien eine höhere Sicherheit zu gewährleisten..
-  **25.00:** 7-Zip für Windows kann jetzt mehr als 64 CPU-Threads für die Kompression nutzen.
-  **24.09:** Die Standardwerte für die Wörterbuchgröße bei den Komprimierungsmethoden LZMA/LZMA2 wurden erhöht.
-  **24.05:** Neuer Filter für RISC-V-Programme.
-  **23.01:** Neuer Filter für ARM64-Programme. BCJ2-Filter wurde für eine bessere Kompressionsrate verbessert. Einige Bugs wurden behoben.
-  **21.07:** Einige kleine Änderungen und Korrekturen.
-  **21.06:** Der Bug in der LZMA-Encoding-Funktion wurde behoben.
-  **21.03 beta:** LZMA-Wörterbuch bis zu 4 GB. Geschwindigkeitsoptimierungen.
-  **21.02 alpha:** Unterstützung für macOS und Linux. Geschwindigkeitsoptimierungen.
-  **19.00:** Stärke der Verschlüsselung für 7z-Archive wurde erhöht.
-  **18.06:** Einige Geschwindigkeitsoptimierungen im LZMA/LZMA2-Code.
-  **18.05:** Einige Geschwindigkeitsoptimierungen im LZMA/LZMA2-Code.
-  **18.01:** Einige Änderungen im LZMA2/xz-Multithreading-Code für Kompression. Einige Fehler wurden behoben.
-  **9.35:** AES-Code und SFX-Module wurden in das SDK integriert.
-  **9.20:** Neues kleines SFX-Modul für Installationsroutinen.
-  **9.11:** Unterstützung für PPMd.
-  **9.04:** Unterstützung für LZMA2 und XZ.
-  **4.62:** LZMA SDK wird Public Domain.

**LZMA / LZMA2** sind die voreingestellte und allgemeine Kompressionsmethoden des :doc:`7z-Formates <7z>` in **7-Zip**. **LZMA** bietet eine hohe Kompressionsrate und sehr schnelle Dekompression, so dass es sich sehr gut für eingebettete Anwendungen eignet. Beispielsweise kann es zur ROM (Firmware)-Kompression benutzt werden.

**LZMA SDK** beinhaltet:

-  **C++**-Quelltext des **LZMA**-Encoder und -Decoder
-  **C++**-Quelltext für **.7z**-Kompression und -Dekompression (reduzierte Version)
-  **ANSI-C**-kompatibler Quelltext für **LZMA/LZMA2/XZ**-Kompression und -Dekompression
-  **ANSI-C**-kompatibler Quelltext für **7z**-Dekompression mit Beispielen
-  **C#**-Quelltext für **LZMA**-Kompression und -Dekompression
-  **Java**-Quelltext für **LZMA**-Kompression und -Dekompression
-  **lzma.exe** zur Kompression und Dekompression von .lzma
-  **7zr.exe** zur Arbeit mit 7z-Archiven (reduzierte Version der 7z.exe von 7-Zip)
-  **SFX-Module** zur Erstellung von selbstextrahierenden Paketen und Installern

Die Quelltexte in **ANSI-C** und **C++** des LZMA SDK sind Teile des Quelltextes von 7-Zip.

Eigenschaften von **LZMA**:

-  Kompressionsgeschwindigkeit: 2–8 MB/s auf einer 4-GHz-CPU mit zwei CPU-Threads.
-  Dekompressionsgeschwindigkeit auf einem einzelnen CPU-Thread:

   -  30–100 MB/s auf moderner 4-GHz-CPU (Intel, AMD, ARM).
   -  5–15 MB/s auf einfacher 1-GHz-RISC-CPU (ARM, MIPS, PowerPC).

-  Nur wenig Arbeitsspeicher zum Dekomprimieren nötig: 8–32 KB + Wörterbuchgröße
-  Geringe Größe beim Entpacken: 2–8 KB (abhängig von Geschwindigkeitsoptimierungen)

Der **LZMA**-Dekoder nutzt nur CPU-Integerbefehle und kann für jede
moderne 32bit-CPU implementiert werden (auf 16bit-CPU mit Abstrichen).

Lizenz
------

**LZMA SDK** steht unter der **Public Domain.**

Jeder darf den originalen LZMA-SDK-Code kopieren, ändern, veröffentlichen, nutzen, kompilieren, verkaufen oder verteilen, sowohl als Quelltext als auch als kompilierte Binärdatei, für jeden Zweck, kommerziell oder nichtkommerziell, unter allen Umständen.

Hinweis: Die Abkürzung LZMA stand ursprünglich für Lempel - Ziv - Markov chain - Arithmetic coding. Vorläufige Versionen von LZMA verwendeten Arithmetic Coding. In der endgültigen Version von LZMA wurde Arithmetic Coding jedoch durch Range Coding ersetzt.

LZMA Links
----------

-  `LZMA bei Wikipedia <https://de.wikipedia.org/wiki/Lempel-Ziv-Markow-Algorithmus>`__
-  `LZMA-Benchmarkergebnisse für verschiedene CPUs <https://www.7-cpu.com/>`__
-  `XZ Utils / LZMA Utils <https://tukaani.org/xz/>`__
-  `Portierung von LZMA SDK auf JAVA, erstellt von einem unabhängigen Entwickler <https://sourceforge.net/projects/p7zip/>`__
-  `Portierung von LZMA SDK auf Pascal (Delphi, Kylix and Freepascal) <https://www.birtles.org.uk/programming/>`__
-  `PyLZMA: Python-Bindings für LZMA <https://www.joachim-bauch.de/projects/python/pylzma/>`__
-  `LZMA Streams in Java <https://contrapunctus.net/league/haques/lzmajio/>`__
-  `Zip-Ada: LZMA auf Ada <https://unzip-ada.sourceforge.net/>`__
