# SPID-Shibboleth-SP

Configurazione di base per registrare un Service Provider Shibboleth in SPID (rif. Regole tecniche SPID [2]).

File:
* shibboleth2.xml
* metadata.xml
* attribute-map.xml

# SAML-SPID vs SAML2int

## shibboleth2.xml

I punti salienti che differiscono da una configurazione standard secondo il profilo SAML2int sono:
* SessionInitiator custom con attributo `NameIDFormat` valorizzato a:
  `urn:oasis:names:tc:SAML:2.0:nameid-format:transient`
* tag `AuthnRequest` con specificato l'attributo `AttributeConsumingServiceIndex` che corrisponde al set di attributi che il Service Provider richiedera' al Identity provider
* tag `RequestedAuthnContext` con indicato il LoA richiesto per il servizio (`AuthnContextClassRef`), ad es.:
  `urn:oasis:names:tc:SAML:2.0:assertion`

## metadata.xml

* Nei tag KeyDescriptor va aggiunto e valorizzato l'attributo `use` (ad es. `signing`)
* Va inserito il tag `AttributeConsumingService` con tutti gli attributi richiesti dal servizio (tag `RequestedAttribute`)

## attribute-map.xml

Vanno inseriti e mappati tutti gli attributi definiti nella tabella attributi AGID [1]

# Riferimenti

[1] Tabella attributi AGID: http://www.agid.gov.it/sites/default/files/regole_tecniche/tabella_attributi_idp_v1_0.pdf

[2] Regole tecniche SPID: http://www.agid.gov.it/sites/default/files/circolari/spid-regole_tecniche_v1.pdf
