.. title: 7-Zip
.. slug: index
.. date: 2021-03-10T11:04:00+02:00
.. tags:
.. category:
.. link:
.. description:
.. type: text
.. pagekind: frontpage

**7-Zip** ist ein Datenkompressionsprogramm mit einer hohen
Kompressionsrate.

**7-Zip 19.00 (21.02.2019) für Windows herunterladen**:

.. list-table::
   :widths: 60 60 124 70
   :header-rows: 1

   * - Link
     - Version
     - Windows
     - Größe
   * - `Download <https://7-zip.org/a/7z1900.exe>`__
     - .exe
     - 32-bit x86
     - 1,2 MB
   * - `Download <https://7-zip.org/a/7z1900-x64.exe>`__
     - .exe
     - 64-bit x86
     - 1,4 MB



**7-Zip 21.02 alpha (06.05.2021) für Windows herunterladen**:

.. list-table::
   :widths: 60 60 124 70
   :header-rows: 1

   * - Link
     - Version
     - Windows
     - Größe
   * - `Download <https://7-zip.org/a/7z2102.exe>`__
     - .exe
     - 32-bit x86
     - 1,2 MB
   * - `Download <https://7-zip.org/a/7z2102-x64.exe>`__
     - .exe
     - 64-bit x86
     - 1,4 MB



**7-Zip 21.00 alpha für Windows ARM64 herunterladen**:

.. list-table::
   :widths: 60 60 124 70
   :header-rows: 1

   * - Link
     - Version
     - Windows
     - Größe
   * - `Download <https://7-zip.org/a/7z2100-arm64.exe>`__
     - .exe
     - 64-bit ARM64
     - 1,5 MB
 

Die Downloadlinks leiten auf die Seiten von 7-zip.org weiter.

Lizenz
------

**7-Zip** ist **freie Software** mit **offenem Quelltext**. Der Großteil des Codes ist unter der **GNU LGPL** lizensiert. Einige Teile des Quelltextes stehen unter der 3-Klausel-BSD-Lizenz. Der unRAR-Code steht zusätzlich unter gewissen Lizenzeinschränkungen. Für weitere Informationen siehe: `7-Zip Lizenz <https://7-zip.org/license.txt>`__.

Sie dürfen 7-Zip auf allen, sogar gewerblich genutzten, Computern benutzen. Dazu müssen Sie 7-Zip weder registrieren noch dafür bezahlen.

Die Hauptfunktionen von 7-Zip
-----------------------------

-  Hohe Kompressionsrate im :doc:`7z` mit **LZMA**- und **LZMA2**-Kompression
-  Unterstützte Formate:

   -  Packen/Entpacken: 7z, XZ, BZIP2, GZIP, TAR, ZIP und WIM
   -  Nur Entpacken: AR, ARJ, CAB, CHM, CPIO, CramFS, DMG, EXT, FAT, GPT, HFS, IHEX, ISO, LZH, LZMA, MBR, MSI, NSIS, NTFS, QCOW2, RAR, RPM, SquashFS, UDF, UEFI, VDI, VHD, VMDK, WIM, XAR und Z.

-  Bei ZIP- und GZIP-Formaten ist die Kompressionsrate von **7-Zip** um etwa 2–10 % besser als die von PKZip oder WinZip
-  Starke Verschlüsselung mit AES-256 im 7z- und ZIP-Format
-  Selbstentpackende 7z-Archive erstellen
-  Integration in das Kontextmenü von Windows
-  Leistungsstarker Dateimanager
-  Leistungsstarke Kommandozeilenversion
-  Plugin für den FAR-Manager verfügbar
-  In 87 Sprachen übersetzt

**7-Zip** läuft auf Windows 10 / 8 / 7 / Vista / XP / 2019 / 2016 / 2012 / 2008 / 2003 / 2000.

`p7zip <https://sourceforge.net/projects/p7zip/>`__ – Port der Kommandozeilenversion von 7-Zip nach Linux/Posix.

Auf `7-Zips SourceForge-Seite <https://sourceforge.net/projects/sevenzip/>`__ finden Sie ein Forum, Fehlerberichte und die Möglichkeit, neue Funktionen vorzuschlagen.

Kompressionsrate
----------------

Wir haben **7-Zip** mit WinRAR 5.20 verglichen.

**DATEIEN:** Mozilla Firefox 34.0.5 für Windows und Google Earth 6.2.2.6613 für Windows.

+-----------------------+-----------------------------------------+-----------------------------------------+
| **Archiver**          | **Mozilla Firefox**                     | **Google Earth**                        |
+                       +-----------------------------------------+-----------------------------------------+
|                       | | **65 Dateien**                        | | **483 Dateien**                       |
|                       | | **85 280 391 Bytes**                  | | **110 700 519 Bytes**                 |
+                       +------------------------+----------------+------------------------+----------------+
|                       | **Komprimierte Größe** | **Verhältnis** | **Komprimierte Größe** | **Verhältnis** |
+=======================+========================+================+========================+================+
| | **7-Zip 9.35**      | **39 357 375**         | **100 %**      | **15 964 369**         | **100 %**      |
| | **-mx**             |                        |                |                        |                |
+-----------------------+------------------------+----------------+------------------------+----------------+
| | WinRAR 5.20         | 41 789 543             | 106 %          | 17 035 432             | 107 %          |
| | -m5 -s -ma5 -md128m |                        |                |                        |                |
+-----------------------+------------------------+----------------+------------------------+----------------+

Die resultierenden Kompressionsraten variieren je nach benutzten Dateien sehr stark. Normalerweise komprimiert **7-Zip** im 7z-Format etwa 30–70 % besser als im ZIP-Format. Und **7-Zip** komprimiert im ZIP-Format 2–10 % besser als die meisten anderen ZIP-kompatiblen Programme.

Der Download von 7-Zip ist kostenlos von dieser Seite möglich. In der letzten Zeit erreichen uns vermehrt Beschwerden über Firmen, die das Programm gegen eine Gebühr zum Download anbieten. :doc:`Weitere Informationen <support>`
