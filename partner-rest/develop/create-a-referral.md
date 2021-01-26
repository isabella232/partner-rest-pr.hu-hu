---
title: Javaslat létrehozása
description: Hozzon létre független vagy megosztott hivatkozásokat a partner API-ban.
ms.date: 05/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 6aab4b5f45030c3c16294b2929b1a6d3086fb951
ms.sourcegitcommit: 3c165938f544ff226cbe11ca21ed5aa00448d9b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2020
ms.locfileid: "97770494"
---
# <a name="create-a-referral"></a>Javaslat létrehozása

A következőkre vonatkozik:

- Partner API

Ez a témakör az átirányítások létrehozását ismerteti. Kétféle [ReferralType](referral-resources.md#referraltype)létezik:

1. Független: Ha egy hivatkozás egy partner számára látható.
2. Shared: Ha egy hivatkozás két, egymással együttműködő fél számára látható. Ha például a Microsoft és egy partner együttes értékesítési ügylettel dolgozik együtt, akkor mindkét fél megoszthatja az átirányítást. További információ: [megosztott hivatkozás létrehozása](#create-a-shared-referral).

## <a name="prerequisites"></a>Előfeltételek

- A [partner API-hitelesítésben](api-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az App + User hitelesítő adataival.

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                  |
|---------|--------------------------------------------------------------|
| **UTÁNI** | <https://api.partner.microsoft.com/v1.0/engagements/referrals> |

### <a name="request-headers"></a>Kérésfejlécek

- További információért lásd: [partner API Rest-fejlécek](headers.md) .

### <a name="request-body"></a>A kérés törzse

Ez a tábla a kérelem törzsének [hivatkozó](referral-resources.md) tulajdonságait írja le egy új hivatkozáshoz.

| Tulajdonság            | Típus                                                                 | Leírás                                                                                                          |
|---------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| Név                | sztring                                                               | Az ajánló neve.                                                                                            |
| ExternalReferenceId | sztring                                                               | Az átirányításhoz tartozó külső azonosító. Például a saját Dynamics 365 ólom vagy a lehetőség azonosítója.                   |
| Állapot              | [ReferralStatus](referral-resources.md#referralstatus)               | Egy [enumerálás](https://docs.microsoft.com/dotnet/api/system.enum) az átirányítási állapotot jelző értékekkel.          |
| Részállapot           | [ReferralSubstatus](referral-resources.md#referralsubstatus)         | Az átirányítási alállapotot jelző értékekkel rendelkező [enumerálás](https://docs.microsoft.com/dotnet/api/system.enum) .       |
| StatusReason        | sztring                                                               | Az állapottal kapcsolatos leíró üzenet. Például magyarázza el, miért vesztette el az átirányítást.                            |
| ReferralType        | [ReferralType](referral-resources.md#referraltype)                   | Az átirányítási típust jelöli. **Szükséges.**                                                                                        |
| Minősítés       | [ReferralQualification](referral-resources.md#referralqualification) | Az ajánló minőségét jelöli.                                                                              |
| CustomerProfile     | [CustomerProfile](referral-resources.md#customerprofile)             | Ügyfél kapcsolattartási adatai.  **Szükséges.**                                                                                      |
| Hozzájárulás             | [Hozzájárulás](referral-resources.md#consent)                             | A hozzájárulási jelzők az információk megosztását más szervezetekkel, és lehetővé teszik a felhasználóknak való kapcsolatfelvételt. **Kötelező megadni.**               |
| Részletek             | [ReferralDetails](referral-resources.md#referraldetails)             | Vásárlói adatok, megjegyzések, ügyleti érték, pénznem zárási dátuma. **Szükséges.**                                                           |
| Csoport                | [Tag](referral-resources.md#member)                               | A partneri szerepvállalásban részt vevő szervezetekben lévő felhasználókat jelöli.                                   |
| InviteContext       | [InviteContext](referral-resources.md#invitecontext)                 | A felhasználó által megadható további információkat jelenít meg egy másik szervezetnek a partneri szerepvállaláshoz való meghívásakor. |
| Cél         | [ReferralTarget](referral-resources.md#target)        | A felhasználó által megadható további információkat jelenít meg egy másik szervezetnek a partneri szerepvállaláshoz való meghívásakor.  |

#### <a name="status--substatus-transition-states"></a>Állapot & állapot átmeneti állapotai

| Állapot | Engedélyezett állapot-váltás | Engedélyezett alállapot            |
|--------|---------------------------|------------------------------|
| Új    | Új, aktív, lezárt       | Függőben, fogadva            |
| Aktív | Aktív, lezárt            | Elfogadva                     |
| Lezárt | Lezárt                    | Megnyert, elveszett, visszautasított, lejárt |

### <a name="request-example"></a>Példa kérésre

```http
POST https://api.partner.microsoft.com/v1.0/engagements/referrals HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

 {
    "name": "Test Cosell Invite_20",
    "status": "New",
    "substatus": "Pending",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Shared",
    "target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-34104-EBB"
        }
    ],
    "customerProfile": {
        "name": "Contoso Customer Inc",
        "address": {
            "addressLine1": "One Microsoft Way",
            "addressLine2": "34",
            "city": "Redmond",
            "state": "WA",
            "postalCode": "98052",
            "country": "US"
        },
        "size": "10to50employees",
        "team": [
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Sue",
                "lastName": "Smith",
                "phoneNumber": "1234567890",
                "email": "sue.smith@contoso.com"
            },
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Joe",
                "lastName": "Hansen",
                "phoneNumber": "4035698759",
                "email": "joe.hansen@contoso.com"
            }
        ],
        "ids": []
    },
    "consent": {
        "consentToToShareInfoWithOthers": true,
        "consentToContact": true
    },
    "details": {
        "notes": "Customer is looking to leverage Dynamics 365 to manage their supply chain. There is also a need to leverage a set of custom apps to enable their business processes.",
        "dealValue": 50000,
        "currency": "USD",
        "closingDateTime": "2018-11-14T00:00:00Z",
        "requirements": {
            "industries": [
                {
                    "id": "Manufacturing"
                }
            ],
            "products": [
                {
                    "id": "Dynamics365Enterprise"
                }
            ],
            "services": [
                {
                    "id": "DeploymentOrMigration"
                }
            ],
            "solutions": [
                {
                    "name": "Dynamics 365 for Field Service",
                    "type": "Category",
                    "id": "Dynamics365forFieldService"
                }
            ]
        }
    },
    "team": [
        {
            "contactPreference": {
                "locale": "en-us",
                "disableNotifications": false
            },
            "firstName": "John",
            "lastName": "Doe",
            "phoneNumber": "1231231234",
            "email": "john.doe@microsoft.com"
        }
    ],
    "inviteContext": {
        "notes": "Hi ABC Partner, hoping you can help this customer. Thanks, John @ Microsoft",
        "invitedBy": {
            "organizationId": "msft"
        }
    }
}
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, ez a metódus a válasz törzsében lévő felszámított [hivatkozó](referral-resources.md) erőforrást adja vissza.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát lásd: [hibakódok](error-codes.md).

### <a name="response-example"></a>Példa válaszra

``` http
{
    "id": "4111fffc-f9ee-4d53-bba6-569135228642",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Contoso Company",
    "name": "Test Cosell Invite_20",
    "externalReferenceId": null,
    "createdDateTime": "2019-02-23T02:05:23.2931817Z",
    "updatedDateTime": "2019-02-23T02:05:23.2931817Z",
    "expirationDateTime": null,
    "status": "Active",
    "substatus": "Accepted",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Shared",
    "eTag": "\"00006d10-0000-0000-0000-5c70aa630000\"",
    "target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-34104-EBB"
        }
    ],
    "customerProfile": {
        "name": "Contoso Customer Inc",
        "address": {
            "addressLine1": "One Microsoft Way",
            "addressLine2": "34",
            "city": "Redmond",
            "state": "WA",
            "postalCode": "98052",
            "country": "US"
        },
        "size": "10to50employees",
        "team": [
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Sue",
                "lastName": "Smith",
                "phoneNumber": "1234567890",
                "email": "sue.smith@contoso.com"
            },
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Joe",
                "lastName": "Hansen",
                "phoneNumber": "4035698759",
                "email": "joe.hansen@contoso.com"
            }
        ],
        "ids": []
    },
    "consent": {
        "consentToToShareInfoWithOthers": true,
        "consentToContact": true
    },
    "details": {
        "notes": "Customer is looking to leverage Dynamics 365 to manage their supply chain. There is also a need to leverage a set of custom apps to enable their business processes.",
        "dealValue": 50000,
        "currency": "USD",
        "requirements": {
            "industries": [
                {
                    "id": "Manufacturing"
                }
            ],
            "products": [
                {
                    "id": "Dynamics365Enterprise"
                }
            ],
            "services": [
                {
                    "id": "DeploymentOrMigration"
                }
            ],
            "solutions": [
                {
                    "name": "Dynamics 365 for Field Service",
                    "type": "Category",
                    "id": "Dynamics365forFieldService"
                }
            ]
        }
    },
    "team": [
        {
            "contactPreference": {
                "locale": "en-us",
                "disableNotifications": false
            },
            "firstName": "John",
            "lastName": "Doe",
            "phoneNumber": "1231231234",
            "email": "john.doe@microsoft.com"
        }
    ],
    "inviteContext": {
        "notes": "Hi ABC Partner, hoping you can help this customer. Thanks, John @ Microsoft",
        "invitedBy": {
            "organizationId": "msft"
        }
    },
    "links": {
        "relatedReferrals": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals?$filter=engagementId eq '37ef26aa-1d15-4533-9f93-a69bd33ab1e5'",
            "method": "GET"
        },
        "self": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals/4111fffc-f9ee-4d53-bba6-569135228642",
            "method": "GET"
        }
    }
}
```

## <a name="create-a-shared-referral"></a>Megosztott hivatkozás létrehozása

A **megosztott** [átirányítási típushoz](referral-resources.md#referraltype)tartozó hivatkozás létrehozásának két lépése van.

1. [Megosztott hivatkozás létrehozása](#create-your-referral)
2. [Csatlakoztatott hivatkozás létrehozása a második fél számára](#create-a-connected-referral)

A következő folyamatábra ezt a két lépést mutatja be egy megosztott hivatkozó létrehozásához.

![A Microsoft partner API-n keresztül összekapcsolt két hivatkozással megosztott átirányítást bemutató folyamatábra](../images/SharedReferral.png)

### <a name="create-your-referral"></a>Az ajánló létrehozása

1. Hozzon létre egy [ReferralType](referral-resources.md#referraltype) -készlettel megosztott hivatkozást.
2. Másolja a **engagementId** a visszatérési válaszból.

[ReferralTarget](referral-resources.md#target) minta az átirányításhoz

```json
"target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-ABC-DEF"
        }
    ]
```

### <a name="create-a-connected-referral"></a>Csatlakoztatott hivatkozás létrehozása

1. Hozzon létre egy másik hivatkozást a Microsoft számára.
2. Adja meg a **enagementId** az átirányításból, hogy azok össze legyenek kötve.

[ReferralTarget](referral-resources.md#target) minta a Microsoft Referral szolgáltatáshoz

```json
"target": [
        {
            "type": "BusinessProfileLocation",
            "id": "msft"
        }
    ]
```