# SPID-Shibboleth-SP

Configurazione di base per registrare un Service Provider Shibboleth in SPID (rif. Regole tecniche SPID [1]).

File:
* shibboleth2.xml
* metadata.xml
* attribute-map.xml

# SAML-SPID vs SAML2int

## shibboleth2.xml

I punti salienti che differiscono da una configurazione standard secondo il profilo SAML2int [2] sono:
* SessionInitiator custom con attributo `NameIDFormat` valorizzato a:

  `urn:oasis:names:tc:SAML:2.0:nameid-format:transient`

* tag `AuthnRequest` con specificato l'attributo `AttributeConsumingServiceIndex` che corrisponde al set di attributi che il Service Provider richiedera' al Identity provider

* tag `RequestedAuthnContext` con indicato il LoA richiesto per il servizio (`AuthnContextClassRef`), ad es.:

  `urn:oasis:names:tc:SAML:2.0:ac:classes:SpidL1`

## metadata.xml

* Nei tag KeyDescriptor va aggiunto e valorizzato l'attributo `use` (ad es. `signing`)
* Va inserito il tag `AttributeConsumingService` con tutti gli attributi richiesti dal servizio (tag `RequestedAttribute`)

## attribute-map.xml

Vanno inseriti e mappati tutti gli attributi definiti nella tabella attributi AGID [3]. Il formato di default previsto dalla tabella AGID e' `basic`, ma con gli IdP di test di SPID potrebbe essere necessario usare `unspecified`, nel caso scommentare le definizioni corrispondenti in `attribute-map.xml`.
 
# Riferimenti
[1] Regole tecniche SPID: http://www.agid.gov.it/sites/default/files/circolari/spid-regole_tecniche_v1.pdf

[2] SAML2int profile v0.2.1 http://saml2int.org/profile/current/

[3] Tabella attributi AGID: http://www.agid.gov.it/sites/default/files/regole_tecniche/tabella_attributi_idp_v1_0.pdf
