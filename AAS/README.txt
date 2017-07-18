Zum Generiern des Nodesets und der Datentypen für openAAS:
Nutze Julians Fork aus dem branch openaas/parser:
https://github.com/JGrothoff/open62541/tree/openaas/parser

Im ordner openaas die neuen XML und sonstigen Dateien vom UA Expert reinkopieren.
- Custom.Opc.Ua.AssetAdministrationShell.bsd manuell erzeugen/anpassen falls sich was an den Datentypen geändert hat. (Florian?)
- datatypes_openaas.txt manuell erzeugen/anpassen falls sich was an den Datentypen geändert hat. (Florian?)
aas.xml anpassen:
- ersetze "uax:" durch ""
- ersetze "ns=1" durch "ns=2" (Notwendig für die korrekte Generierung der Datentypen von Input/Output Argumenten)

Aus dem Quellverzeichnis des Repositories heraus:
cp -rf AAS/filesToReplace/* .
mkdir build
cd build
cmake ..
ccmake .
- UA_ENABLE_AMALGAMATION OFF
- UA_BUILD_EXAMPLES_NODESET_COMP ON
- UA_BUILD_EXAMPLES OFF
make
ccmake .
- UA_BUILD_EXAMPLES ON
make

In build/openaas_generated/ finden sich die generierten Dateien.
Mit dem Beispiel examples/server_nodeset kann das Laden des Nodesets überprüft werden.

Zur Generierung des open62541.c und .h files (mit NS0) wurde der commit 2ed2a9e0e642a2957e081a1bae927a469523f4f5 aus dem nodestore_switch Branch bei Julian genutzt.
