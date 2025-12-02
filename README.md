# Webservice de consulta de deutes de multes per a ajuntaments

## Procediment d’adhesió
1. Descarregar el [formulari d'adhesió](https://github.com/organisme-de-gestio-tributaria/consulta-deutes-multes/blob/main/Formulari%20d'adhesi%C3%B3.pdf). Si no es visualitza al navegador, descarregueu-lo al vostre dispositiu.
2. Emplenar el formulari.
3. El formulari l'ha de signar l'Alcalde/ssa.
3. Enviar el formulari signat via EACAT a l’ORGT.

## Informació tècnica

Cal accedir al webservice mitjançat l'endpoint REST. L’especificació es pot obtenir del [fitxer swagger disponible en aquest repositori](https://github.com/organisme-de-gestio-tributaria/consulta-deutes-multes/blob/main/swagger%20DeutesMultes.json).

El servei es troba a les següents URL's:
* Producció: https://wsreal.orgt.diba.cat/DeutesMultes/DeutesMultesService.svc/rest
* Pre-produció (proves): https://wsproves.orgt.diba.cat/DeutesMultes/DeutesMultesService.svc/rest

Respecte a la seguretat, cal tenir en compte:
1. L’accés al web service serà via https i amb certificat d'òrgan. 
1. Es comprovarà que les dades enviades corresponen a l’Ajuntament associat al certificat. Per fer les proves també cal fer servir un certificat d'òrgan.
1. **Previ a les proves cal comunicar el certificat utilitzat a l’ORGT ja que és necessari instal·lar la clau pública als servidors de la ORGT.** Vegeu el procediment d'adhesió a l'inici d'aquest web, els detalls estan en el formulari d'adhesió.

Els endpoints disponibles són:
1. **GenerarDocument** Permet generar els documents acreditatius de que un DNI/NIF té o no té deutes de multes amb l'ajuntament. Cal introduir:
   - CodiINE10: codi INE10 de l'ajuntament
   - DNINIFContribuent: DNI/NIF del contribuent (8 dígits, sense la lletra de control)
   - Idioma: Idioma del document final (C: català o E: castellà)
1. **ObtenirLlistaDeutes** Permet consultar la llista de deutes d'un DNI/NIF amb l'ajuntament. Cal introduir:
   - CodiINE10: codi INE10 de l'ajuntament
   - DNINIFContribuent : DNI/NIF del contribuent (8 dígits, sense la lletra de control)
   - Idioma. C: català o E: castellà


## Exemples de crides i respostes
A continuació es presenten diversos exemples de crides i respostes. Podeu trobar més informació a:
* **[Especificació swagger](https://github.com/organisme-de-gestio-tributaria/consulta-deutes-multes/blob/main/swagger%20DeutesMultes.json). Podeu crear el vostre client de forma automàtica a partir d'aquest fitxer.**
* L’esquema de validació de les dades rebudes es troba en el mateix webservice a: https://wsproves.orgt.diba.cat/DeutesMultes/schema/DeutesMultes.xsd 
* Cal notar que totes les dades de tipus text han d'estar en majúscules.

| Endpoint | Mètode HTTP | Exemples |
|---|---|---|
| GenerarDocument | GET | [URL petició](https://wsproves.orgt.diba.cat/DeutesMultes/DeutesMultesService.svc/rest/GenerarDocument?DNINIFContribuent=00000000&CodiINE10Municipi=0810170005&Idioma=C) <br> [Resposta](https://github.com/organisme-de-gestio-tributaria/consulta-deutes-multes/blob/main/Exemples/respostaGenerarDocument.json)
| ObtenirLlistaDeutes | GET | [URL petició](https://wsproves.orgt.diba.cat/DeutesMultes/DeutesMultesService.svc/rest/ObtenirDeutes?DNINIFContribuent=00000000&CodiINE10Municipi=0810170005&Idioma=C) <br> [Resposta](https://github.com/organisme-de-gestio-tributaria/consulta-deutes-multes/blob/main/Exemples/respostaObtenirDeutes.json)



