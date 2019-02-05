**ATTENZIONE: Questo repository non e' piu' manutenuto. Per informazioni ufficiali su SPID e Shibboleth SP vedi:**
 * https://github.com/italia/spid-sp-shibboleth
 * https://github.com/italia/spid-auth-docker


# SPID-Shibboleth-SP

Configurazione di base per registrare un Service Provider Shibboleth in SPID (rif. Regole tecniche SPID [1], Errata 
Corrige 24/06/2016 [2] e Documento riassuntivo del 29/07/2016 [5]).

File:
* shibboleth2.xml
* metadata.xml
* attribute-map.xml

# SAML-SPID vs SAML2int

## shibboleth2.xml

I punti salienti che differiscono da una configurazione standard secondo il profilo SAML2int [3] sono:
* SessionInitiator custom con attributo `NameIDFormat` valorizzato a:

  `urn:oasis:names:tc:SAML:2.0:nameid-format:transient`

* tag `AuthnRequest` con specificato l'attributo `AttributeConsumingServiceIndex` che corrisponde al set di attributi che il Service Provider richiedera' al Identity provider

* tag `RequestedAuthnContext` con indicato il LoA richiesto per il servizio (`AuthnContextClassRef`), ad es.:

  `<saml:AuthnContextClassRef>https://www.spid.gov.it/SpidL1</saml:AuthnContextClassRef>`

## metadata.xml

* Nei tag KeyDescriptor va aggiunto e valorizzato l'attributo `use` (ad es. `signing`)
* Va inserito il tag `AttributeConsumingService` con tutti gli attributi richiesti dal servizio (tag `RequestedAttribute`)

## attribute-map.xml

Vanno inseriti e mappati tutti gli attributi definiti nella tabella attributi AGID [4]. Il formato di default previsto dalla tabella AGID e' `basic`, ma con gli IdP di test di SPID potrebbe essere necessario usare `unspecified`, nel caso aggiungere le definizioni corrispondenti in `attribute-map.xml`.
 
# Riferimenti
[1] Regole tecniche SPID: http://www.agid.gov.it/sites/default/files/circolari/spid-regole_tecniche_v1.pdf

[2] REGOLAMENTO RECANTE LE REGOLE TECNICHE – Errata Corrige (Avviso nr. 5 24 giugno 2016): http://www.agid.gov.it/sites/default/files/documentazione/spid-avviso-n5-regole-tecniche-errata-corrige.pdf

[3] SAML2int profile v0.2.1: http://saml2int.org/profile/current/

[4] Tabella attributi AGID: http://www.agid.gov.it/sites/default/files/regole_tecniche/tabella_attributi_idp_v1_0.pdf

[5] Documento riassuntivo per la preparazione del metadato (29/07/2016): http://www.agid.gov.it/sites/default/files/documentazione/spid-avviso-n6-note-sul-dispiegamento-di-spid-presso-i-gestori-di-servizi-v1.pdf
