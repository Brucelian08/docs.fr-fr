---
title: Protocoles de messagerie
ms.date: 03/30/2017
ms.assetid: 5b20bca7-87b3-4c8f-811b-f215b5987104
ms.openlocfilehash: 3e56636e8364eec333f9585a0f62f6510561d1cc
ms.sourcegitcommit: c7f3e2e9d6ead6cc3acd0d66b10a251d0c66e59d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/09/2018
ms.locfileid: "44253063"
---
# <a name="messaging-protocols"></a>Protocoles de messagerie
La pile de canal Windows Communication Foundation (WCF) utilise des canaux de transport et de codage pour transformer la représentation interne de message dans son format câble et l’envoyer à l’aide d’un transport particulier. Le transport le plus couramment utilisé pour l'interopérabilité des services Web est le HTTP, et les encodages les plus couramment utilisés par les services Web sont SOAP 1.1 basé sur XML, SOAP 1.2 et MTOM (Message Transmission Optimization Mechanism).  
  
 Cette rubrique traite des détails d’implémentation de WCF pour les protocoles suivants utilisés par <xref:System.ServiceModel.Channels.HttpTransportBindingElement>.  
  
|Spécification/document|Link|  
|-----------------------------|----------|  
|HTTP 1.1|http://www.ietf.org/rfc/rfc2616.txt|  
|Liaison HTTP SOAP 1.1|http://www.w3.org/TR/2000/NOTE-SOAP-20000508/, Section 7|  
|Liaison HTTP SOAP 1,2|http://www.w3.org/TR/soap12-part2/, Section 7|  
  
 Cette rubrique traite des détails d’implémentation de WCF pour les protocoles suivants utilisés qui <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> et <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement> employer.  
  
|Spécification/Document|Link|  
|-----------------------------|----------|  
|XML|http://www.w3.org/TR/REC-xml|  
|SOAP 1,1|http://www.w3.org/TR/2000/NOTE-SOAP-20000508/|  
|SOAP 1.2 Core|http://www.w3.org/TR/soap12-part1/|  
|WS-Addressing 2004/08|http://www.w3.org/Submission/2004/SUBM-ws-addressing-20040810/|  
|W3C Web Services Addressing 1.0 – Éléments principaux|http://www.w3.org/TR/2006/REC-ws-addr-core-20060509|  
|W3C Web Services Addressing 1.0 – Liaison SOAP|http://www.w3.org/TR/2006/REC-ws-addr-soap-20060509|  
|W3C Web Services Addressing 1.0 – Liaison WSDL|http://www.w3.org/TR/2006/CR-ws-addr-wsdl-20060529/|  
W3C Web Services Addressing 1.0 - Métadonnées|http://www.w3.org/TR/ws-addr-metadata/|  
|Liaison WSDL SOAP 1.1|http://www.w3.org/TR/wsdl/|  
|Liaison WSDL SOAP 1.2|http://www.w3.org/Submission/wsdl11soap12/|  
  
 Cette rubrique traite des détails d’implémentation de WCF pour les protocoles suivants utilisés qui <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement> utilise.  
  
|Spécification/document|Link|  
|-----------------------------|----------|  
|XOP|http://www.w3.org/TR/xop10/|  
|Liaison MTOM + SOAP 1.2|http://www.w3.org/TR/soap12-mtom/|  
|Liaison MTOM SOAP 1.1|http://www.w3.org/Submission/soap11mtom10/|  
|Assertion de MTOM WS-Policy|http://www.w3.org/Submission/2006/SUBM-WS-MTOMPolicy-20061101/.|  
  
 Les espaces de noms XML suivants et les préfixes associés sont utilisés dans l'ensemble de cette rubrique.  
  
|Préfixe|URI (Uniform Resource Identifier) de l'espace de noms|  
|------------|---------------------------------------------------|  
|s11|http://schemas.xmlsoap.org/soap/envelope|  
|s12|http://www.w3.org/2003/05/soap-envelope|  
|wsa|http://www.w3.org/2004/08/addressing|  
|wsam|http://www.w3.org/2007/05/addressing/metadata|  
|wsap|http://schemas.xmlsoap.org/ws/2004/09/policy/addressing|  
|wsa10|http://www.w3.org/2005/08/addressing|  
|wsaw10|http://www.w3.org/2006/05/addressing/wsdl|  
|xop|http://www.w3.org/2004/08/xop/include|  
|xmime|http://www.w3.org/2004/06/xmlmime<br /><br /> http://www.w3.org/2005/05/xmlmime|  
point de distribution|http://schemas.microsoft.com/net/2006/06/duplex|  
  
## <a name="soap-11-and-soap-12"></a>SOAP 1.1 et SOAP 1.2  
  
### <a name="envelope-and-processing-model"></a>Enveloppe et modèle de traitement  
 WCF implémente le traitement de l’enveloppe SOAP 1.1 suivant Basic Profile 1.1 (BP11) et Basic Profile 1.0 (SSBP10). Le traitement d'enveloppe SOAP 1.2 est implémenté selon SOAP12-Part1.  
  
 Cette section explique certaines options d’implémentation prises par WCF quant à BP11 et SOAP12-Part1.  
  
#### <a name="mandatory-header-processing"></a>Traitement obligatoire des en-têtes  
 WCF suit les règles de traitement des en-têtes marqués `mustUnderstand` décrit dans les spécifications SOAP 1.1 et SOAP 1.2, avec les variations suivantes.  
  
 Un message qui entre dans la pile de canal WCF est traité par les canaux individuels configurés par les éléments de liaison associés, par exemple, l’encodage de Message texte, sécurité, une messagerie fiable et les Transactions. Chaque canal reconnaît les en-têtes de l'espace de noms associé et les marque comme compris. Une fois qu'un message entre le répartiteur, le module de formatage de l'opération lit les en-têtes attendus par le contrat de message/opération correspondant et les marque comme compris. Ensuite, le répartiteur vérifie si des en-têtes restants ne sont pas compris mais marqués comme `mustUnderstand` et lève une exception. Les messages qui contiennent des en-têtes `mustUnderstand` ciblant le destinataire ne sont pas traités par le code de l'application destinataire.  
  
 Un tel traitement par couches permet de séparer les couches d'infrastructure et les couches d'application du nœud SOAP :  
  
-   B1111 : Les en-têtes qui ne sont pas compris sont détectés après que le message est traité par la pile de canaux d’infrastructure WCF, mais avant son traitement par application  
  
     La valeur d'en-tête `mustUnderstand` diffère entre SOAP 1.1 et SOAP 1.2. Basic Profile 1.1 exige que la valeur `mustUnderstand` soit définie sur 0 ou 1 pour les messages SOAP 1.1. SOAP 1.2 accepte les valeurs 0, 1, `false` et `true`, mais recommande d'émettre une représentation canonique de valeurs `xs:boolean` (`false`, `true`).  
  
-   B1112 : WCF émet `mustUnderstand` valeurs 0 et 1 pour les versions SOAP 1.1 et SOAP 1.2 de l’enveloppe SOAP. WCF accepte l’espace de valeur entière de `xs:boolean` pour le `mustUnderstand` en-tête (0, 1, `false`, `true`)  
  
#### <a name="soap-faults"></a>Erreurs SOAP  
 Voici une liste d’implémentations de d’erreur SOAP de WCF spécifique.  
  
-   B2121 : WCF retourne les Codes d’erreur SOAP 1.1 suivantes : `s11:mustUnderstand`, `s11:Client`, et `s11:Server`.  
  
-   B2122 : WCF retourne les Codes d’erreur SOAP 1.2 suivants : `s12:MustUnderstand`, `s12:Sender`, et `s12:Receiver`.  
  
### <a name="http-binding"></a>Liaison HTTP  
  
#### <a name="soap-11-http-binding"></a>Liaison HTTP SOAP 1.1  
 WCF implémente la liaison HTTP SOAP1.1 en suivant la spécification Basic Profile 1.1 section 3.4 avec les éclaircissements suivants :  
  
-   B2211 : Le service WCF n’implémente pas la redirection des demandes HTTP POST.  
  
-   B2212 : Les clients WCF prennent en charge les Cookies HTTP conformément à 3.4.8.  
  
#### <a name="soap-12-http-binding"></a>Liaison HTTP SOAP 1,2  
 WCF implémente la liaison SOAP 1.2 HTTP comme décrit la spécification SOAP, 1.2-partie 2 (SOAP12Part2) avec les éclaircissements suivants.  
  
 SOAP 1.2 a introduit un paramètre d'action facultatif pour le type de média `application/soap+xml`. Ce paramètre est utile pour optimiser la distribution du message sans que le corps du message SOAP soit analysé lorsque la spécification WS-Addressing n'est pas utilisée.  
  
-   R2221 : le paramètre d'action `application/soap+xml`, lorsqu'il est présent dans une demande SOAP 1.2, doit correspondre à l'attribut `soapAction` sur l'élément `wsoap12:operation` dans la liaison WSDL correspondante.  
  
-   R2222 : le paramètre d'action `application/soap+xml`, lorsqu'il est présent dans un message SOAP 1.2, doit correspondre à `wsa:Action` lorsque la spécification WS-Addressing 2004/08 ou WS-Addressing 1.0 est utilisée.  
  
 Lorsque la spécification WS-Addressing est désactivée et qu'une demande entrante ne contient pas de paramètre d'action, l'`Action` du message est considérée comme non spécifiée.  
  
## <a name="ws-addressing"></a>WS-Addressing  
 WCF implémente 3 versions de WS-Addressing :  
  
-   WS-Addressing 2004/08  
  
-   W3C Web Services Addressing 1.0 Core (ADDR10-CORE) et liaison SOAP (ADDR10-SOAP)  
  
-   WS-Addressing 1.0 - Métadonnées  
  
### <a name="endpoint-references"></a>Références de point de terminaison  
 Toutes les versions de WS-Addressing qui implémente de WCF utilisent des références de point de terminaison pour décrire des points de terminaison.  
  
#### <a name="endpoint-references-and-ws-addressing-versions"></a>Références de point de terminaison et versions de WS-Addressing  
 WCF implémente plusieurs protocoles d’infrastructure qui utilisent WS-Addressing et en particulier le `EndpointReference` élément et `W3C.WsAddressing.EndpointReferenceType` classe (par exemple, WS-ReliableMessaging, WS-SecureConversation et WS-Trust). WCF prend en charge l’utilisation de des versions de WS-Addressing avec d’autres protocoles d’infrastructure. Points de terminaison WCF prend en charge une version de WS-Addressing par point de terminaison.  
  
 Pour R3111, l’espace de noms pour le `EndpointReference` élément ou type utilisé dans les messages échangés avec un point de terminaison WCF doit correspondre à la version de WS-Addressing implémentée par ce point de terminaison.  
  
 Par exemple, si un point de terminaison WCF implémente WS-ReliableMessaging, le `AcksTo` en-tête retourné par ce point de terminaison à l’intérieur de `CreateSequenceResponse` utilise la version de WS-Addressing qui le `EncodingBinding` élément spécifie pour ce point de terminaison.  
  
#### <a name="endpoint-references-and-metadata"></a>Références de point de terminaison et métadonnées  
 Plusieurs scénarios nécessitent de communiquer des métadonnées ou une référence aux métadonnées pour un point de terminaison donné.  
  
 B3121 : WCF utilise les mécanismes décrits dans la spécification WS-MetadataExchange (MEX) Section 6 pour inclure les métadonnées pour les références de point de terminaison par valeur ou par référence.  
  
 Imaginez un scénario où un service WCF requiert une authentification à l’aide d’un jeton de Security Assertions Markup Language (SAML) émis par l’émetteur du jeton à http://sts.fabrikam123.com. Le point de terminaison WCF décrit cette exigence d’authentification à l’aide de `sp:IssuedToken` assertion avec imbriquée `sp:Issuer` assertion pointant vers l’émetteur du jeton. Les applications clientes qui accèdent à l'assertion `sp:Issuer` doivent savoir comment communiquer avec l'émetteur du jetons du point de terminaison. Le client a besoin de connaître les métadonnées relatives à l'émetteur de jetons. Utilisez les extensions de métadonnées de référence de point de terminaison définies dans MEX, WCF fournit une référence aux métadonnées de l’émetteur du jeton.  
  
```xml  
<sp:IssuedToken>  
  <sp:Issuer>  
    <wsa10:Address>  
      http://sts.fabrikam123.com  
    </wsa10:Address>  
    <wsa10:Metadata>  
      <mex:Metadata>  
        <mex:MetadataSection>  
          <mex:MetadataReference>  
            <wsa10:Address>  
              http://sts.fabrikam123.com/mex  
            </wsa10:Address>  
          </mex:MetadataReference>  
        </mex:MetadataSection>  
      </mex:Metadata>  
    </wsa10:Metadata>  
  </sp:Issuer>  
</sp:IssuedToken>  
```  
  
### <a name="message-addressing-headers"></a>En-têtes d'adressage des messages  
  
#### <a name="message-headers"></a>En-têtes de message  
 Pour les deux versions de WS-Addressing, WCF utilise les en-têtes de message suivants comme le prescrivent les spécifications `wsa:To`, `wsa:ReplyTo`, `wsa:Action`, `wsa:MessageID`, et `wsa:RelatesTo`.  
  
 B3211 : Pour toutes les versions de WS-Addressing, WCF respecte mais ne produit pas dès le départ, les en-têtes de message WS-Addressing `wsa:FaultTo` et `wsa:From`.  
  
 Applications qui interagissent avec les applications WCF peuvent ajouter que ces en-têtes et message WCF les traitera en conséquence.  
  
#### <a name="reference-parameters-and-properties"></a>Paramètres et propriétés de référence  
 WCF implémente le traitement des paramètres de référence de point de terminaison et de référence p  
  
 conformément aux spécifications respectives.  
  
 B3221 : Quand est configuré pour utiliser WS-Addressing 2004/08, les points de terminaison WCF ne distinguent pas des propriétés de référence et les paramètres de référence de traitement.  
  
### <a name="message-exchange-patterns"></a>Modèles d’échange de messages  
 La séquence de messages impliquées dans l’appel d’opération de service Web est appelée le *modèle d’échange de message*. Modèles d’échange de messages duplex, demande-réponse et prend en charge WCF unidirectionnel. Cette section clarifie les exigences WS-Addressing de traitement des messages en fonction du modèle d’échange de messages utilisé.  
  
 Dans cette section, le demandeur envoie le premier message et le répondeur reçoit le premier message.  
  
#### <a name="one-way-message"></a>Message unidirectionnel  
 Quand un point de terminaison WCF est configuré pour prendre en charge des messages avec une donnée `Action` pour suivre un modèle unidirectionnel, le point de terminaison WCF suit les comportements et les conditions requises suivantes. Sauf indication contraire, les comportements et les règles s’appliquent pour les deux versions de WS-Addressing prises en charge dans WCF :  
  
-   R3311 : le demandeur doit inclure `wsa:To`, `wsa:Action` et les en-têtes pour tous les paramètres de référence spécifiés par la référence de point de terminaison. Lorsque WS-Addressing 2004/08 est utilisée et que des [propriétés de référence] sont spécifiées par la référence de point de terminaison, les en-têtes correspondants doivent également être ajoutés au message.  
  
-   B3312: le demandeur peut inclure les en-têtes `MessageID`, `ReplyTo` et `FaultTo`. L'infrastructure du récepteur les ignorera, et ils seront passés à l'application.  
  
-   R3313: lorsque le HTTP est utilisé et qu'aucun message n'est envoyé sur la section de réponse HTTP, le répondeur doit envoyer une réponse HTTP avec un corps vide et un code d'état HTTP 202.  
  
     Lorsque le transport HTTP est utilisé et que le contrat d'opération déclare un message unidirectionnel, la réponse HTTP peut encore être utilisée pour envoyer les messages d'infrastructure. Par exemple, la messagerie fiable peut envoyer un message `SequenceAcknowledgement` sur une réponse HTTP.  
  
-   B3314 : Le répondeur WCF n’envoie pas d’un message d’erreur en réponse à un message unidirectionnel.  
  
#### <a name="request-reply"></a>Demande-réponse  
 Lorsqu’un point de terminaison WCF est configuré pour un message avec une donnée `Action` pour suivre le modèle demande-réponse, le point de terminaison WCF suit les comportements et les exigences ci-dessous. Sauf indication contraire, les comportements et les règles s’appliquent pour les deux versions de WS-Addressing prises en charge dans WCF :  
  
-   R3321 : Le demandeur doit inclure dans la demande `wsa:To`, `wsa:Action`, `wsa:MessageID`et les en-têtes pour tous les paramètres de référence ou référence propriétés (ou les deux) spécifiés par la référence de point de terminaison.  
  
-   R3322 : lorsque WS-Addressing 2004/08 est utilisée, `ReplyTo` doit également être inclus dans la demande.  
  
-   R3323 : Lorsque WS-Addressing 1.0 est utilisée et `ReplyTo` n’est pas présent dans la demande, une référence de point de terminaison par défaut avec la propriété [adresse] égale à « http://www.w3.org/2005/08/addressing/anonymous» est utilisé.  
  
-   R3324 : Le demandeur doit inclure `wsa:To`, `wsa:Action`, et `wsa:RelatesTo` en-têtes du message de réponse, ainsi que les en-têtes pour tous les paramètres de référence ou référence propriétés (ou les deux) spécifié par le `ReplyTo` référence de point de terminaison dans le demande.  
  
### <a name="web-services-addressing-faults"></a>Erreurs d'adressage des services Web  
 R3411 : WCF génère les erreurs suivantes définies par WS-Addressing 2004/08.  
  
|Code|Cause|  
|----------|-----------|  
|wsa:DestinationUnreachable|Le message est arrivé avec un `ReplyTo` différent de l'adresse de réponse établie pour ce canal ; il n'y a aucun point de terminaison qui écoute l'adresse spécifiée dans l'en-tête To.|  
|wsa:ActionNotSupported|les canaux de l'infrastructure ou le répartiteur associé au point de terminaison ne reconnaissent pas l'action spécifiée dans l'en-tête `Action`.|  
  
 R3412 : WCF génère les erreurs suivantes définies par WS-Addressing 1.0.  
  
|Code|Cause|  
|----------|-----------|  
|wsa10:InvalidAddressingHeader|Dupliquer `wsa:To`, `wsa:ReplyTo`, `wsa:From` ou `wsa:MessageID`. Dupliquer `wsa:RelatesTo` avec le même `RelationshipType`.|  
|wsa10:MessageAddressingHeaderRequired|L'en-tête d'adressage requis est absent.|  
|wsa10:DestinationUnreachable|Le message est arrivé avec un `ReplyTo` différent de l'adresse de réponse établie pour ce canal. Il n'y a aucun point de terminaison qui écoute l'adresse spécifiée dans l'en-tête To.|  
|wsa10:ActionNotSupported|Une action spécifiée dans l'en-tête `Action` n'est pas reconnue par les canaux de l'infrastructure ou le répartiteur associé au point de terminaison.|  
|wsa10:EndpointUnavailable|Le canal RM renvoie cette erreur pour indiquer que le point de terminaison ne traitera pas la séquence suite à l'examen des en-têtes d'adressage du message `CreateSequence`.|  
  
 Le code des tables précédentes correspond à `FaultCode` dans SOAP 1.1 et `SubCode` (avec Code=Expéditeur) dans SOAP 1.2.  
  
### <a name="wsdl-11-binding-and-ws-policy-assertions"></a>Liaison WSDL 1.1 et assertions de WS-Policy  
  
#### <a name="indicating-use-of-ws-addressing"></a>Utilisation recommandée de WS-Addressing  
 WCF utilise les assertions de stratégie pour indiquer la prise en charge de point de terminaison pour une version particulière de WS-Addressing.  
  
 L'assertion de stratégie suivante possède l'objet de stratégie de point de terminaison [WS-PA] et indique que les messages envoyés et reçus depuis le point de terminaison doivent utiliser WS-Addressing 2004/08.  
  
```xml  
<wsap:UsingAddressing />  
```  
  
 Cette assertion de stratégie complète la spécification WS-Addressing 2004/08.  
  
 L'assertion de stratégie indique que les messages envoyés/reçus doivent utiliser WS-Addressing 1.0.  
  
```xml
<wsam:Addressing/>   
```  
  
 L'assertion de stratégie suivante possède un objet de stratégie de point de terminaison [WS-PA] et indique que les messages envoyés et reçus depuis le point de terminaison doivent utiliser WS-Addressing 2004/08.  
  
```xml  
<wsaw10:UsingAddressing />  
```  
  
 L'élément `wsaw10:UsingAddressing` est emprunté à [WS-Adressage-WSDL] et est utilisé dans le contexte de WS-Policy conformément à la section 3.1.2 de cette spécification.  
  
 L’utilisation de l’adressage n’altère pas la sémantique des liaisons HTTP WSDL 1.1, SOAP 1.1 et SOAP 1.2. Par exemple, si une réponse est attendue à une demande envoyée à un point de terminaison qui utilise l’adressage et la liaison HTTP WSDL SOAP 1.x, elle doit être envoyée en utilisant la réponse HTTP.  
  
 Pour les réponses envoyées via HTTP, l'assertion WS-AM est :  
  
```xml  
<wsam:AnonymousResponses/>  
```  
  
 L'assertion de stratégie complète peut ressembler à ceci :  
  
```xml  
<wsam:Addressing>  
    <wsp:Policy>  
        <wsam:AnonymousResponses />   
    </wsp:Policy>  
</wsam:Addressing>  
```  
  
 Toutefois, certains modèles d’échange de messages profitent du fait que deux connexions HTTP réciproques indépendantes soient établies entre le demandeur et le répondeur, par exemple dans le cas de messages unidirectionnels non sollicités envoyés par le répondeur.  
  
 WCF offre une fonctionnalité par lequel deux canaux de transport sous-jacents peuvent former un canal Duplex Composite, où un canal est utilisé pour les messages d’entrée et l’autre est utilisée pour les messages de sortie. Dans le cas du transport HTTP, le canal duplex composite fournit deux connexions HTTP réciproques. Le demandeur utilise une connexion pour envoyer des messages au répondeur, et le répondeur utilise l'autre pour renvoyer des messages au demandeur.  
  
 Pour les réponses envoyées via des demandes HTTP distinctes, l'assertion WS-AM est :  
  
```xml  
<wsam:NonAnonymousResponses/>  
```  
  
 L'assertion de stratégie complète peut ressembler à ceci :  
  
```xml  
<wsam:Addressing>  
    <wsp:Policy>  
      <wsam:NonAnonymousResponses />   
   </wsp:Policy>  
  </wsam:Addressing>  
```  
  
 Pour utiliser l’assertion suivante, qui possède un objet de stratégie de point de terminaison [WS-PA] sur les points de terminaison qui utilisent des liaisons HTTP WSDL 1.1 SOAP 1.x, il est nécessaire d’utiliser deux connexions HTTP réciproques séparées pour transmettre des messages du demandeur au répondeur et du répondeur au demandeur, respectivement.  
  
```xml  
<cdp:CompositeDuplex/>  
```  
  
 L'instruction précédente mène aux spécifications suivantes pour l'en-tête `wsa:ReplyTo` des messages de demande :  
  
-   R3514 : Messages de demande envoyés à un point de terminaison doivent avoir un `ReplyTo` en-tête avec le `[address]` propriété différente de « http://www.w3.org/2005/08/addressing/anonymous» si le point de terminaison utilise une liaison de WSDL 1.1 SOAP 1.x HTTP et utilise une alternative de stratégie avec un `wsap10:UsingAddressing` ou `wsap:UsingAddressing` assertion couplée avec `cdp:CompositeDuplex` attaché.  
  
-   R3515 : Messages de demande envoyés à un point de terminaison doivent avoir un `ReplyTo` en-tête avec le `[address]` propriété égale à « http://www.w3.org/2005/08/addressing/anonymous», ou n'avez pas un `ReplyTo` en-tête du tout, si le point de terminaison utilise une liaison de WSDL 1.1 SOAP 1.x HTTP et utilise une alternative de stratégie avec `wsap10:UsingAddressing` assertion et aucune `cdp:CompositeDuplex` assertion attachée.  
  
-   R3516 : Messages de demande envoyés à un point de terminaison doivent avoir un `ReplyTo` en-tête avec un `[address]` propriété égale à « http://www.w3.org/2005/08/addressing/anonymous» si le point de terminaison utilise une liaison de WSDL 1.1 SOAP 1.x HTTP et utilise une alternative de stratégie avec `wsap:UsingAddressing` assertion et aucun `cdp:CompositeDuplex`assertion attachée.  
  
 La spécification WSDL de WS-Addressing tente de décrire des liaisons de protocole semblables en présentant un élément `<wsaw:Anonymous/>` avec trois valeurs textuelles (obligatoire, facultatif et a interdit) pour indiquer des besoins sur l'en-tête `wsa:ReplyTo` (section 3.2). Malheureusement, une telle définition d'élément n'est pas particulièrement utilisable comme une assertion dans le contexte de WS-Policy, car il requiert que les extensions spécifiques au domaine prennent en charge l'intersection d'alternatives à l'aide d'un élément de ce type comme une assertion. Une telle définition d'élément indique également la valeur de l'en-tête `ReplyTo` par opposition au comportement du point de terminaison sur la transmission, ce qui le rend spécifique au transport HTTP.  
  
#### <a name="action-definition"></a>Définition d'action  
 WS-Addressing 2004/08 définit un attribut `wsa:Action` pour les éléments `wsdl:portType/wsdl:operation/[wsdl:input | wsdl:output | wsdl:fault]`. La liaison WS-Addressing 1.0 WSDL (WS-ADDR10-WSDL) définit un attribut semblable, `wsaw10:Action`.  
  
 La seule différence entre les deux réside dans la sémantique du modèle d’action par défaut décrite à la section 3.3.2 de WS-ADDR et à la section 4.4.4 de WS-ADDR10-WSDL, respectivement.  
  
 Il est raisonnable d’avoir deux points de terminaison qui partagent le même `portType` (ou contrat, dans la terminologie WCF), mais à l’aide de différentes versions de WS-Addressing. Mais étant donné que cette action est définie par le `portType` et ne doit pas pour les points de terminaison qui implémentent le `portType`, il devient impossible de prendre en charge les deux modèles d'action par défaut.  
  
 Pour résoudre ce conflit, WCF prend en charge une seule version de la `Action` attribut.  
  
 B3521 : WCF utilise le `wsaw10:Action` attribut sur `wsdl:portType/wsdl:operation/[wsdl:input | wsdl:output | wsdl:fault]` éléments tel que défini dans WS-ADDR10-WSDL pour déterminer le `Action` URI pour les messages correspondants, quelle que soit la version de WS-Addressing utilisée par le point de terminaison.  
  
#### <a name="use-endpoint-reference-inside-wsdl-port"></a>Utilisation des références de point de terminaison à l'intérieur d'un port WSDL  
 La section 4.1 de WS-ADDR10-WSDL étend l'élément `wsdl:port` de manière à inclure l'élément enfant `<wsa10:EndpointReference…/>` et décrire le point de terminaison en des termes propres à WS-Addressing. WCF étend cette fonctionnalité à WS-Addressing 2004/08, ce qui permet `<wsa:EndpointReference…/>` à apparaissent sous la forme d’un élément enfant de `wsdl:port`.  
  
-   R3531 : si un point de terminaison possède une alternative de stratégie attachée avec une assertion de la stratégie `<wsaw10:UsingAddressing/>`, l'élément `wsdl:port` correspondant peut contenir un élément enfant `<wsa10:EndpointReference …/>`.  
  
-   R3532 : Si un `wsdl:port` contient un élément enfant `<wsa10:EndpointReference …/>`, le `wsa10:EndpointReference/wsa10:Address` valeur de l’élément enfant doit correspondre à la valeur de la `@address` attribut du frère `wsdl:port` / `wsdl:location` élément.  
  
-   R3533 : si un point de terminaison possède une alternative de stratégie attachée avec une assertion de la stratégie `<wsap:UsingAddressing/>`, l'élément `wsdl:port` correspondant peut contenir un élément enfant `<wsa:EndpointReference …/>`.  
  
-   R3534 : Si un `wsdl:port` contient un élément enfant `<wsa:EndpointReference …/>`, le `wsa:EndpointReference/wsa:Address` valeur de l’élément enfant doit correspondre à la valeur de la `@address` attribut du frère `wsdl:port` / `wsdl:location` élément.  
  
### <a name="composition-with-ws-security"></a>Composition avec WS-Security  
 D'après les sections relatives à la sécurité de WS-ADDR et WS-ADDR10, il est recommandé que tous les en-têtes d'adressage de messages soient signés avec le corps du message afin de les lier.  
  
 Lorsque WS-Security est utilisée pour la protection de l'intégrité des messages, les en-têtes de message WS-Addressing ainsi que les en-têtes résultant des paramètres ou des propriétés de référence (ou les deux) doivent être signés avec le corps du message.  
  
### <a name="examples"></a>Exemples  
  
#### <a name="one-way-message"></a>Message unidirectionnel  
 Dans ce scénario, l'expéditeur envoie un message unidirectionnel au récepteur. SOAP 1.2, HTTP 1.1 et W3C WS-Addressing 1.0 sont utilisés.  
  
 Structure du message de demande : les en-têtes de message incluent les éléments `wsa10:To` et `wsa10:Action`. Le corps du message inclut un élément `<app:Ping>` spécifique de l'espace de noms de l'application.  
  
 En-têtes HTTP : La destination dans POST correspond à l’URI dans le `wsa10:To` élément.  
  
 L'en-tête Content-Type a la valeur `application/soap+xml` comme l'exige SOAP 1.2. Les paramètres `charset` et `action` sont inclus. Le paramètre `action` de l'en-tête Content-Type correspond à la valeur de l'en-tête de message `wsa10:Action`.  
  
```  
POST http://fabrikam123.com/Service HTTP/1.1  
Content-Type: application/soap+xml; charset=utf-8;    
              action="http://fabrikam123.com/Service/OneWay"  
Host: 131.107.72.15  
Content-Length: 1501  
Expect: 100-continue  
Proxy-Connection: Keep-Alive  
<s12:Envelope>  
  <s12:Header>  
    <wsa10:To s12:mustUnderstand="1">  
        http://fabrikam123.com/Service  
    </wsa10:To>  
    <wsa10:Action s12:mustUnderstand="1">  
        http://fabrikam123.com/Service/OneWay   
    </wsa10:Action>  
  </s12:Header>  
  <s12:Body>  
    <Ping xmlns="http://fabrikam123.com/Service/">  
      <Text>Hello World</Text>  
    </Ping>  
  </s12:Body>  
</s12:Envelope>  
```  
  
 Le récepteur répond avec une réponse HTTP vide et l'état 202. Exemple de réponse HTTP :  
  
```  
HTTP/1.1 202 Accepted  
Date: Fri, 15 Jul 2005 08:56:07 GMT  
Server: Microsoft-IIS/6.0  
MicrosoftOfficeWebServer: 5.0_Pub  
X-Powered-By: ASP.NET  
X-AspNet-Version: 2.0.50215  
Cache-Control: private  
Content-Length: 0  
```  
  
## <a name="soap-message-transmission-optimization-mechanism"></a>SOAP MTOM (Message Transmission Optimization Mechanism)  
 Cette section décrit les détails d’implémentation de WCF pour le protocole MTOM HTTP SOAP. Technologie MTOM est mécanisme d’encodage SOAP message de la même classe que l’encodage de texte/XML traditionnel ou l’encodage binaire WCF. MTOM inclut ce qui suit :  
  
-   Un mécanisme d'encodage XML et d'empaquetage décrit par [XOP] qui optimise les éléments d'information XML qui contiennent les données binaires encodées en Base64 dans des parties binaires séparées.  
  
-   Encapsulation MIME du package XOP qui sérialise l'ensemble d'informations XML et chaque partie binaire du package XOP dans une partie MIME séparée.  
  
-   Encodage XOP MIME appliqué à l'enveloppe SOAP 1.x.  
  
-   Liaison de transport HTTP.  
  
 Il est possible d’utiliser MTOM avec des transports non-HTTP avec WCF. Toutefois, nous nous concentrerons sur le HTTP dans cette rubrique.  
  
 Le format MTOM tire parti d'un grand ensemble de spécifications qui couvrent MTOM lui-même, XOP et MIME. La modularité de cet ensemble de spécifications rend quelque peu difficile la reconstruction des spécifications exactes sur le format et le traitement de la sémantique. Cette section décrit les spécifications de format et de traitement pour la liaison HTTP MTOM.  
  
### <a name="mtom-message-encoding"></a>Encodage de message MTOM  
  
#### <a name="generating-mtom-messages"></a>Génération de messages MTOM  
 Le [XOP] la section 3.1 décrit le processus de l'encodage XML avec des détails d'élément qui contiennent des valeurs Base64 dans un package XOP abstraitement défini.  
  
 La séquence d'étapes suivante décrit le processus d'encodage spécifique à MTOM :  
  
1.  Assurez-vous que l’enveloppe SOAP à encoder ne contient aucune information sur l’élément avec un `[namespace name]` de « http://www.w3.org/2004/08/xop/include» et un `[local name]` de `Include`.  
  
2.  Créez un package MIME vide.  
  
3.  Identifiez dans l'ensemble d'informations XML d'origine les éléments à optimiser. Pour les éléments à optimiser, les caractères qui composent le `[children]` de l’élément d’information élément doit être dans la forme canonique de `xs:base64Binary` (voir XSD-2, 3.2.16 base64Binary) et ne doit pas contenir les caractères d’espace blanc précédent, inline avec, ou suivant le contenu autre qu’un espace blanc.  
  
4.  Créez une enveloppe SOAP XOP qui est une copie de l'enveloppe SOAP d'origine, mais en remplaçant les enfants de chaque élément d'information identifiés à l'étape précédente par un élément d'information `xop:Include` construit comme suit :  
  
    1.  Transformez les caractères remplacés en données binaires en les traitant comme des données encodées en Base64.  
  
    2.  Générez une valeur d'en-tête Content-ID unique qui satisfait aux spécifications R3133 et R3134.  
  
    3.  Générez un en-tête MIME Content-Transfer-Encoding avec la valeur binaire.  
  
    4.  Si l'élément d'information qui est optimisé (le [parent] de l'élément d'information `xop:Include` inséré) a un élément d'information d'attribut `xmime:contentType`, générez un en-tête MIME Content-type avec la valeur de l'attribut `xmime:contentType`.  
  
    5.  Générez une nouvelle partie MIME binaire avec le contenu formé par les données binaires décodées des caractères remplacés traités en Base64, l'en-tête Content-ID de l'étape 4b, l'en-tête Content-Transfer-Encoding de l'étape 4c, l'en-tête Content-Type si généré à l'étape 4d.  
  
    6.  Ajoutez un attribut `href` à l'élément `xop:Include` avec la valeur cid : l'uri dérivé de la valeur d'en-tête Content-ID générée à l'étape 4b. Supprimer la forme «\<» et « > » caractères, URL d’échappement la chaîne restante et ajoutez le préfixe `cid:`. Le jeu de caractères minimum suivant est requis pour un échappement par RFC1738 et RFC2396. D'autres caractères peuvent faire l'objet d'une séquence d'échappement.  
  
        ```  
        Hexadecimal 00-1F , 7F, 20, "<" | ">" | "#" | "%" | <">  
        "{" | "}" | "|" | "\" | "^" | "[" | "]" | "`" | "~" | "^"  
        ```  
  
5.  Créez une partie MIME racine avec l'enveloppe SOAP XOP à partir de l'étape 4.  
  
6.  Écrivez les en-têtes HTTP, y compris l'en-tête HTTP Content-Type.  
  
7.  Écrivez le package MIME.  
  
#### <a name="processing-mtom-messages"></a>Traitement des messages MTOM  
 Le traitement d'un message MTOM est l'inverse exact du processus décrit dans la section précédente « Génération de messages MTOM » :  
  
1.  Vérifiez que la partie MIME racine possède le `application/xop+xml` Content-type.  
  
2.  Construisez une enveloppe SOAP en analysant la partie MIME racine du package comme un document XML. L'encodage de caractères est déterminé par le paramètre `charset` du Content-type de la partie MIME racine.  
  
3.  Pour chaque élément d'information dans l'enveloppe SOAP construite, qui a comme seul membre de sa propriété [enfant] un élément d'information `xop:Include` :  
  
    1.  Supprimez le préfixe `cid:` préfixent et annulez toutes les séquences d'échappement d'URI (RFC 2396) dans la valeur de l'attribut `@href` de l'élément `xop:Include`. Placez la chaîne de résultat dans «\<», « > ».  
  
    2.  Localisez la partie MIME avec la valeur d'en-tête Content-ID qui correspond à la chaîne dérivée à l'étape 3a.  
  
    3.  Remplacez l'élément d'information `xop:Include` qui apparaît dans la propriété `children` de chaque élément par les éléments d'information de caractère qui représentent l'encodage Base64 canonique (voir XSD-2, 3.2.16 base64Binary) du corps d'entité de la partie MIME identifiée à l'étape 3b (remplacez l'élément d'information `xop:Include` par les données reconstruites à partir de la partie du package).  
  
#### <a name="http-content-type-header"></a>En-tête HTTP Content-Type  
 Voici une liste d’éclaircissements WCF pour le format de l’en-tête HTTP Content-Type d’un message encodé en MTOM de SOAP 1.x dérivé des exigences indiquées dans la spécification MTOM elle-même et est dérivé de MTOM et RFC 2387.  
  
-   R4131 : un en-tête HTTP Content-Type doit avoir la valeur de multipart/related (non sensible à la casse) et ses paramètres. Les noms des paramètres ne respectent pas la casse. L'ordre des paramètres n'est pas important.  
  
-   La forme Backus-Naur (BNF) complète de l'en-tête Content-Type pour les messages MIME est répertoriée dans RFC 2045, section 5.1.  
  
-   R4132 : un en-tête Content-Type HTTP doit avoir un paramètre de type avec la valeur `application/xop+xml` comprise entre des guillemets doubles.  
  
 Alors que la nécessité d’utiliser des guillemets doubles n’est pas explicite dans RFC 2387, le texte observe que tous les paramètres de type média multipart/related contiennent très probablement des caractères réservés tels que «\@» ou « / » et, par conséquent guillemet double marque.  
  
-   R4133 : un en-tête HTTP Content-Type doit avoir un paramètre de début avec la valeur de l'en-tête Content-ID de la partie MIME qui contient l'enveloppe SOAP 1.x, entourée de guillemets doubles. Si le paramètre de début est omis, la première partie MIME doit contenir l'enveloppe SOAP 1.x.  
  
-   R4134 : un en-tête HTTP Content-Type pour un message SOAP 1.1 encodé en MTOM doit inclure le paramètre start-info avec la valeur de texte/xml, entouré par des guillemets doubles.  
  
-   R4135 : un en-tête Content-Type HTTP pour un message SOAP 1.2 encodé en MTOM doit inclure le paramètre start-info avec la valeur de `application/soap+xml`, entre des guillemets doubles.  
  
-   R4136 : l'en-tête HTTP Content-Type d'un message SOAP 1.x encodé en MTOM doit avoir le paramètre de limite avec la valeur (entourée par des guillemets doubles) qui correspond au BNF de limite MIME défini dans RFC 2046, section 5.1.1  
  
    ```  
    boundary := 0*69<bchars> bcharsnospace   
    bchars := bcharsnospace / " "   
    bcharsnospace :=    DIGIT / ALPHA / "'" / "(" / ")" / "+"   
                        / "_" / "," / "-" / "." / "/" / ":" / "=" / "?"  
    ```  
  
     Exemples :  
  
     CORRECT  
  
    ```  
    Content-Type: multipart/related; type="application/xop+xml";start=" <part0@tempuri.org>";boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1";start-info="text/xml"  
    ```  
  
     CORRECT  
  
    ```  
    Content-Type: Multipart/Related; type="application/xop+xml";start-info="text/xml";boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1"  
    ```  
  
     INCORRECT  
  
    ```  
    Content-Type: Multipart/Related; type=application/xop+xml;start=" <part0@tempuri.org>";start-info="text/xml";boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1"   
    ```  
  
#### <a name="infoset-mime-part"></a>Partie MIME d'ensemble d'informations  
 L'enveloppe SOAP 1.x est encapsulée comme une partie racine du package MIME XOP et est souvent appelée la partie `infoset`.  
  
-   R4141 : l'enveloppe SOAP 1.x doit être encapsulée comme une partie racine du package MIME XOP, appelée la partie `infoset` et référencée depuis le Content-Type HTTP.  
  
-   R4142 : la partie SOAP `Infoset` doit inclure les en-têtes MIME suivants : `Content-ID`, `Content-Transfer-Encoding` et `Content-Type`.  
  
 Le format de l'en-tête Content-ID est défini par RFC 2045 comme  
  
```  
"Content-ID" ":" msg-id  
```  
  
 où `msg-id` est défini dans RFC 2822 (remplace RFC 822, référencé dans RFC 2045) comme :  
  
```  
msg-id    =       [CFWS] "<" id-left "@" id-right ">" [CFWS]  
```  
  
 et est effectivement une adresse de messagerie encadrée par «\<» et « > ». Les préfixe et suffixe `[CFWS]` ont été ajoutés dans RFC 2822 pour contenir des commentaires et ne doivent pas être utilisés pour préserver l'interopérabilité.  
  
 R4143 : la valeur de l'en-tête Content-ID pour la partie MIME de l'ensemble d'informations doit suivre la production `msg-id` de RFC 2822 avec les parties `[CFWS]` préfixe et suffixe omises.  
  
 Plusieurs implémentations MIME ont assoupli des exigences pour la valeur placée dans »\<» et « > » pour être une adresse de messagerie et utilisé `absoluteURI` placés entre »\<», « > » en plus de l’adresse de messagerie. Cette version de WCF utilise les valeurs de l’en-tête MIME Content-ID du formulaire :  
  
```  
Content-ID: <http://tempuri.org/0>   
```  
  
 R4144 : les processeurs MTOM doivent accepter les valeurs d'en-tête Content-ID qui correspondent au `msg-id` assoupli suivant.  
  
```  
msg-id-relaxed =     [CFWS] "<" (absoluteURI | mail-address) ">" [CFWS]  
mail-address   =     id-left "@" id-right  
```  
  
 MIME (RFC 2045) fournit l'en-tête Content-Transfer-Encoding pour communiquer l'encodage du contenu de la partie MIME. La valeur par défaut définie pour Content-Transfer-Encoding est de 7 bits, ce qui ne convient pas à la plupart des messages SOAP ; l'en-tête Content-Transfer-Encoding est donc nécessaire pour une plus grande interopérabilité :  
  
-   R4145 : la partie de l'ensemble d'informations SOAP doit contenir l'en-tête Content-Transfer-Encoding.  
  
-   R4146 : si l'encodage de caractères de l'enveloppe SOAP est UTF-8, la valeur de l'en-tête Content-Transfer-Encoding doit être de 8 bits.  
  
-   R4147 : si l'encodage de caractères de l'enveloppe SOAP est UTF-16, la valeur de l'en-tête Content-Transfer-Encoding doit être binaire.  
  
-   D'après [XOP] section 5,  
  
-   R4148 : Partie de l’ensemble d’informations SOAP1.1 doit contenir l’en-tête Content-Type avec le type de média application/xop + xml et les paramètres de type = « text/xml » et le jeu de caractères  
  
    ```  
    Content-Type: application/xop+xml;  
                  charset=utf-8;type="text/xml"  
    ```  
  
-   R4149 : La partie de l’ensemble d’informations SOAP 1.2 doit contenir l’en-tête Content-Type avec le type de média `application/xop+xml` et paramètres de type = «`application/soap+xml`» et `charset`.  
  
    ```  
    Content-Type: application/xop+xml;  
                  charset=utf-8;type="application/soap+xml"  
    ```  
  
     Bien que XOP définisse le paramètre `charset` de manière à ce que `application/xop+xml` soit facultatif, il est exigé pour l'interopérabilité comme la spécification BP 1.1 sur le paramètre `charset` pour le type de média `text/xml`.  
  
-   R41410 : Les paramètres `type` et `charset` doivent être présents dans l'en-tête Content-Type de la partie de l'ensemble d'informations SOAP 1.x.  
  
#### <a name="wcf-endpoint-support-for-mtom"></a>Prise en charge des points de terminaison WCF pour MTOM  
 L'objectif de MTOM est d'encoder un message SOAP pour optimiser les données encodées en Base64. Les contraintes sont répertoriées dans la liste suivante :  
  
-   R4151 : tout élément d'information qui contient des données encodées en Base64 peut être optimisé.  
  
-   B4152 : WCF optimise les éléments d’information qui contiennent des données codées en base64 et dépassent 1024 octets.  
  
 Un point de terminaison WCF configuré pour utiliser MTOM enverra toujours des messages encodés MTOM. Même si aucune partie ne répond aux critères requis, le message est tout de même encodé en MTOM (sérialisé comme un package MIME avec une partie MIME unique qui contient l'enveloppe SOAP).  
  
### <a name="ws-policy-assertion-for-mtom"></a>Assertion de WS-Policy pour MTOM  
 WCF utilise l’assertion de stratégie suivante pour indiquer l’utilisation MTOM par point de terminaison :  
  
```xml  
<wsoma:OptimizedMimeSerialization ... />  
```  
  
-   R4211 : l'assertion de stratégie précédente a un objet de stratégie de point de terminaison et spécifie que tous les messages envoyés et reçus depuis le point de terminaison doivent être optimisés à l'aide de MTOM.  
  
-   B4212 : Quand est configuré pour utiliser l’optimisation MTOM, un point de terminaison WCF ajoute une assertion de stratégie MTOM à la stratégie attachée correspondant `wsdl:binding`.  
  
### <a name="composition-with-ws-security"></a>Composition avec WS-Security  
 MTOM est un mécanisme d’encodage qui est similaire à `text/xml` et XML binaire WCF. MTOM offre la composition naturelle avec WS-Security et d'autre protocoles WS-* : un message sécurisé à l'aide de WS-Security peut être optimisé à l'aide de MTOM.  
  
### <a name="examples"></a>Exemples  
  
#### <a name="wcf-soap-11-message-encoded-using-mtom"></a>Message SOAP 1.1 WCF encodé à l'aide de MTOM  
  
```  
POST http://131.107.72.15/Mtom/svc/service.svc/Soap11MtomUTF8 HTTP/1.1  
SOAPAction: "http://xmlsoap.org/echoBinaryAsString"  
Content-Type: multipart/related;type="application/xop+xml";  
              start="<http://tempuri.org/0>";start-info="text/xml";  
       boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1"  
Host: 131.107.72.15  
Content-Length: 1501  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1  
Content-ID: <http://tempuri.org/0>  
Content-Transfer-Encoding: 8bit  
Content-Type: application/xop+xml;charset=utf-8;type="text/xml"  
<s:Envelope xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">  
  <s:Body>  
    <EchoBinaryAsString xmlns="http://xmlsoap.org/Ping">  
      <array>  
        <xop:Include   
         href="cid:http%3A%2F%2Ftempuri.org%2F1%2F632618206521093670"   
         xmlns:xop="http://www.w3.org/2004/08/xop/include"/>  
      </array>  
    </EchoBinaryAsString>  
  </s:Body>  
</s:Envelope>  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1  
Content-ID: <http://tempuri.org/1/632618206521093670>  
Content-Transfer-Encoding: binary  
Content-Type: application/octet-stream  
…Binary Content..  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1  
```  
  
#### <a name="wcf-secure-soap-12-message-encoded-using-mtom"></a>Message sécurisé SOAP 1.2 WCF encodé à l'aide de MTOM  
 Dans cet exemple, un message est encodé à l'aide de MTOM et SOAP 1.2 et protégé à l'aide de WS-Security. Les parties binaires identifiées pour l'encodage sont les contenus du `BinarySecurityToken`, `CipherValue` des `EncryptedData` correspondant à la signature chiffrée et au corps chiffré. Notez que le `CipherValue` de la `EncryptedKey` a été pas été identifiée pour l’optimisation par WCF, car sa longueur est inférieure à 1024 octets.  
  
```  
POST http://131.107.72.15/Mtom/service.svc/Soap12MtomSecureSignEncrypt HTTP/1.1  
Content-Type: multipart/related; type="application/xop+xml";  
              start="<http://tempuri.org/0>";  
            boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3";  
              start-info="application/soap+xml";   
              action="http://xmlsoap.org/echoBinaryAsString"  
Host: 131.107.72.15  
Content-Length: 1941  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3  
Content-ID: <http://tempuri.org/0>  
Content-Transfer-Encoding: 8bit  
Content-Type: application/xop+xml;charset=utf-8;type="application/soap+xml"  
<s:Envelope xmlns:s="http://schemas.xmlsoap.org/soap/envelope/" xmlns:u="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">  
  <s:Header>  
    <o:Security s:mustUnderstand="1" xmlns:o="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd">  
      <u:Timestamp u:Id="uuid-4d4ee765-5717-4d53-9ac9-99bddc07df6c-5">  
        <u:Created>2005-09-09T06:57:32.488Z</u:Created>  
        <u:Expires>2005-09-09T07:02:32.488Z</u:Expires>  
      </u:Timestamp>  
      <o:BinarySecurityToken u:Id="uuid-4d4ee765-5717-4d53-9ac9-99bddc07df6c-2" ValueType="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-x509-token-profile-1.0#X509v3" EncodingType="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-soap-message-security-1.0#Base64Binary">  
        <xop:Include href="cid:http%3A%2F%2Ftempuri.org%2F1%2F632618206525089430" xmlns:xop="http://www.w3.org/2004/08/xop/include"/>  
      </o:BinarySecurityToken>  
      <e:EncryptedKey Id="_1" xmlns:e="http://www.w3.org/2001/04/xmlenc#">  
        <e:EncryptionMethod Algorithm="http://www.w3.org/2001/04/xmlenc#rsa-oaep-mgf1p"/>  
        <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">  
          <o:SecurityTokenReference>  
            <o:KeyIdentifier ValueType="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-x509-token-profile-1.0#X509SubjectKeyIdentifier">Xeg55vRyK3ZhAEhEf+YT0z986L0=</o:KeyIdentifier>  
          </o:SecurityTokenReference>  
        </KeyInfo>  
        <e:CipherData>          <e:CipherValue>oQfpxwT8/SAGyZQzKE2b4yO6dXuQj7pwJ+5CGL3Rf7C06bQ5ttMoQ9GLJcQYkXTzin+WwHEgs5bj5ml9HKTW9QAU5JJ6lksdymmQvWP5ZtGPBVchO4sofEGoCKmBiZL/DYS/cnbzgnc/3a6NYnc10y2fWGaGLiqa00zijAw7o0Y=</e:CipherValue>  
        </e:CipherData>  
      </e:EncryptedKey>  
      <c:DerivedKeyToken u:Id="_2" xmlns:c="http://schemas.xmlsoap.org/ws/2005/02/sc">  
        <o:SecurityTokenReference>  
          <o:Reference URI="#_1"/>  
        </o:SecurityTokenReference>  
        <c:Nonce>OrEPRX7fISIS4sXYWPMv3g==</c:Nonce>  
      </c:DerivedKeyToken>  
      <e:ReferenceList xmlns:e="http://www.w3.org/2001/04/xmlenc#">  
        <e:DataReference URI="#_3"/>  
        <e:DataReference URI="#_4"/>  
      </e:ReferenceList>  
      <e:EncryptedData Id="_4" Type="http://www.w3.org/2001/04/xmlenc#Element" xmlns:e="http://www.w3.org/2001/04/xmlenc#">  
        <e:EncryptionMethod Algorithm="http://www.w3.org/2001/04/xmlenc#aes256-cbc"/>  
        <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">  
          <o:SecurityTokenReference>  
            <o:Reference URI="#_2"/>  
          </o:SecurityTokenReference>  
        </KeyInfo>  
        <e:CipherData>  
          <e:CipherValue>  
            <xop:Include href="cid:http%3A%2F%2Ftempuri.org%2F2%2F632618206525089430" xmlns:xop="http://www.w3.org/2004/08/xop/include"/>  
          </e:CipherValue>  
        </e:CipherData>  
      </e:EncryptedData>  
    </o:Security>  
  </s:Header>  
  <s:Body u:Id="_0">  
    <e:EncryptedData Id="_3" Type="http://www.w3.org/2001/04/xmlenc#Content" xmlns:e="http://www.w3.org/2001/04/xmlenc#">  
      <e:EncryptionMethod Algorithm="http://www.w3.org/2001/04/xmlenc#aes256-cbc"/>  
      <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">  
        <o:SecurityTokenReference xmlns:o="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd">  
          <o:Reference URI="#_2"/>  
        </o:SecurityTokenReference>  
      </KeyInfo>  
      <e:CipherData>  
        <e:CipherValue>  
          <xop:Include href="cid:http%3A%2F%2Ftempuri.org%2F3%2F632618206525089430" xmlns:xop="http://www.w3.org/2004/08/xop/include"/>  
        </e:CipherValue>  
      </e:CipherData>  
    </e:EncryptedData>  
  </s:Body>  
</s:Envelope>  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3  
Content-ID: <http://tempuri.org/1/632618206525089430>  
Content-Transfer-Encoding: binary  
Content-Type: application/octet-stream  
...Binary content of BinarySecurityToken - X509 Certificate...  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3  
Content-ID: <http://tempuri.org/2/632618206525089430>  
Content-Transfer-Encoding: binary  
Content-Type: application/octet-stream  
...Binary serialization of the encrypted primary signature...  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3  
Content-ID: <http://tempuri.org/3/632618206525089430>  
Content-Transfer-Encoding: binary  
Content-Type: application/octet-stream  
...Binary serialization of the encrypted Body...  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3--  
```
