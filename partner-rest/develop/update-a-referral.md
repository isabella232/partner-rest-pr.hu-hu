---
title: Érdeklődő vagy lehetőség frissítése (elavult)
description: Lehetővé teszi az érdeklődő vagy a lehetőség részleteinek frissítését. Ez a módszer egy érdeklődő vagy lehetőség frissítésére elavult, és ehelyett a recommmend használja.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 9705db1c21dbec7099cfefebdc7bb23ec65e428c
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770543"
---
# <a name="update-a-lead-or-opportunity-obsolete"></a>Érdeklődő vagy lehetőség frissítése (elavult)

A következőkre vonatkozik:

- Partner API

Ez a témakör azt ismerteti, hogyan frissítheti az érdeklődők vagy a lehetőségek részleteit, például az ügylet értékét, a becsült zárási dátumot, illetve az értékesítési fázisok kezelését a további részletek között. 


> [!IMPORTANT]
Ez a módszer egy érdeklődő vagy lehetőség frissítésére elavult, és [Ehelyett a recommmend](patch-a-referral.md) használja.

## <a name="prerequisites"></a>Előfeltételek

- A [partner API-hitelesítésben](api-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az App + User hitelesítő adataival.
- Ez az API jelenleg csak a felhasználói hozzáférést támogatja, ahol a partnereknek a következő szerepkörök egyikében kell lenniük: globális rendszergazda, hivatkozó rendszergazda vagy hivatkozó felhasználó.

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                       |
|---------|-------------------------------------------------------------------|
| **PUT** | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}> |

### <a name="request-headers"></a>Kérésfejlécek

- További információ: [partner API Rest-fejlécek](headers.md).

> [!IMPORTANT]
> Ügyeljen arra, hogy az **IF-Match** fejlécet adja meg.

### <a name="request-body"></a>A kérés törzse

Ez a táblázat a kérés törzsének [hivatkozó](referral-resources.md) tulajdonságait ismerteti.

| Tulajdonság            | Típus                                                                 | Leírás                                                                                                          |
|---------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| Id                  | sztring                                                               | Az átirányításhoz tartozó azonosító.                                                                                            |
| EngagementId        | sztring                                                               | Az ajánló EngagementID. Több hivatkozás is társítható egyetlen EngagementID                    |
| Name                | sztring                                                               | Az ajánló neve.                                                                                            |
| ExternalReferenceId | sztring                                                               | Az átirányításhoz tartozó külső azonosító. Példa: saját Dynamics 365 érdeklődő/lehetőség AZONOSÍTÓjának tárolása                    |
| CreatedDateTime     | karakterlánc UTC-dátum időformátuma                                       | Az átirányítás létrehozásának dátuma.                                                                                   |
| UpdatedDateTime     | karakterlánc UTC-dátum időformátuma                                       | Az átirányítás utolsó frissítésének dátuma.                                                                              |
| ExpirationDateTime  | karakterlánc UTC-dátum időformátuma                                       | Az átirányítás érvényességének dátuma.                                                                                   |
| Állapot              | [ReferralStatus](referral-resources.md#referralstatus)               | Egy [enumerálás](https://docs.microsoft.com/dotnet/api/system.enum) az átirányítási állapotot jelző értékekkel.          |
| Részállapot           | [ReferralSubstatus](referral-resources.md#referralsubstatus)         | Az átirányítási alállapotot jelző értékekkel rendelkező [enumerálás](https://docs.microsoft.com/dotnet/api/system.enum) .      |
| StatusReason        | sztring                                                               | Az állapottal kapcsolatos leíró üzenet. Például magyarázza el, miért vesztette el az átirányítást.                              |
| ReferralType        | [ReferralType](referral-resources.md#referraltype)                   | Az átirányítási típust jelöli.                                                                                        |
| Minősítés       | [ReferralQualification](referral-resources.md#referralqualification) | Az ajánló minőségét jelöli.                                                                              |
| CustomerProfile     | [CustomerProfile](referral-resources.md#customerprofile)             | Ügyfél kapcsolattartási adatai.                                                                                        |
| Hozzájárulás             | [Hozzájárulás](referral-resources.md#consent)                             | A hozzájárulási jelzők az információk megosztását más szervezetekkel, és lehetővé teszik a felhasználóknak való kapcsolatfelvételt.                |
| Részletek             | [ReferralDetails](referral-resources.md#referraldetails)             | Vásárlói adatok, megjegyzések, ügyleti érték, pénznem zárási dátuma.                                                          |
| Csoport                | [Tag](referral-resources.md#member)                               | A partneri szerepvállalásban részt vevő szervezetekben lévő felhasználókat jelöli.                                   |
| InviteContext       | [InviteContext](referral-resources.md#invitecontext)                 | A felhasználó által megadható további információkat jelenít meg egy másik szervezetnek a partneri szerepvállaláshoz való meghívásakor. |
| Cél         | [ReferralTarget](referral-resources.md#target)        | A felhasználó által megadható további információkat jelenít meg egy másik szervezetnek a partneri szerepvállaláshoz való meghívásakor.  |

### <a name="status-and-substatus-transition-states"></a>Állapot-és alállapot-áttérési állapotok

| Állapot | Engedélyezett állapot-váltás | Engedélyezett alállapot            |
|--------|---------------------------|------------------------------|
| Új    | Új, aktív, lezárt       | Függőben, fogadva            |
| Aktív | Aktív, lezárt            | Elfogadva                     |
| Lezárt | Lezárt                    | Megnyert, elveszett, visszautasított, lejárt |

### <a name="request-example"></a>Példa kérésre

```http
PUT https://api.partner.microsoft.com/v1.0/engagements/referrals/49d90c72-3326-4f61-aacc-2cb57970448c HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

 {
    "id": "49d90c72-3326-4f61-aacc-2cb57970448c",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "createdDateTime": "2018-11-06T18:40:42.6178337Z",
    "updatedDateTime": "2018-11-06T18:40:42.6178337Z",
    "expirationDateTime": "2018-11-14T00:00:00Z",
    "status": "Closed",
    "substatus": "Won",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Independent",
    "target": [
        {
            "type": "BusinessProfileLocation",
            "id": "01e2abcd-52b0-4af3-a3ae-1fd1530b3563"
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
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\"",

}
```

> [!IMPORTANT]
> Távolítsa el az `"links": { }` objektumot az Put erőforrásból.

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, ez a metódus a válasz törzsében lévő felszámított [hivatkozó](referral-resources.md) erőforrást adja vissza.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát lásd: [hibakódok](error-codes.md).

### <a name="response-example"></a>Példa válaszra

``` http
{
    "id": "4111fffc-f9ee-4d53-bba6-569135228642",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Contoso Company",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "createdDateTime": "2018-11-06T18:40:42.6178337Z",
    "updatedDateTime": "2018-11-06T18:43:38.9948636Z",
    "expirationDateTime": "2018-11-14T00:00:00Z",
    "status": "Closed",
    "substatus": "Won",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Independent",
    "target": [
        {
            "type": "BusinessProfileLocation",
            "id": "01e2abcd-52b0-4af3-a3ae-1fd1530b3563"
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
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\"",
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