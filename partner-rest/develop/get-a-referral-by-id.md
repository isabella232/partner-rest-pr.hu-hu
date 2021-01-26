---
title: Érdeklődő vagy lehetőség lekérése azonosító alapján
description: Érdeklődő vagy lehetőség beszerzése azonosító alapján.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: dcfaea393afc6a9d09946b4c31b7168ba26aa255
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770531"
---
# <a name="get-a-lead-or-opportunity-by-id"></a>Érdeklődő vagy lehetőség lekérése azonosító alapján

A következőkre vonatkozik:

- Partner API

Ez a témakör azt ismerteti, hogyan lehet az azonosító alapján érdeklődői vagy közös értékesítési lehetőséget szerezni.

> [!Note]
> A Microsoft kereskedelmi piactérről (Azure Marketplace és AppSource) kapott érdeklődők nem támogatottak. 

## <a name="prerequisites"></a>Előfeltételek

- A [partner API-hitelesítésben](api-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az App + User hitelesítő adataival.
- Ez az API jelenleg csak a felhasználói hozzáférést támogatja, ahol a partnereknek a következő szerepkörök egyikében kell lenniük: globális rendszergazda, hivatkozó rendszergazda vagy hivatkozó felhasználó.

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus   | Kérés URI-ja                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **GET** | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}>                                     |

### <a name="uri-parameter"></a>URI-paraméter


| Név                   | Típus     | Kötelező | Leírás                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Id                      | sztring   | Igen       | Az érdeklődő vagy a közös értékesítés lehetőség egyedi azonosítója       |

### <a name="request-headers"></a>Kérésfejlécek

További információért lásd: [partner Rest-fejlécek](headers.md) .

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id} HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, a válasz törzse tartalmazza az azonosítóhoz tartozó [érdeklődőt vagy lehetőséget](referral-resources.md) .

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy [http-állapotkód](error-codes.md) , amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek beolvasásához használjon hálózati nyomkövetési eszközt.

### <a name="response-example"></a>Példa válaszra

``` http
HTTP/1.1 200 OK
Content-Type: application/json
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731

{
    "@odata.context": "https://api.partner.microsoft.com/v1.0/engagments/referrals/$metadata#Referrals/$entity",
    "id": "c5fbb3b6-be74-4795-9fb5-4324c73fed37",
    "engagementId": "65edc0b5-3485-41b7-a17e-dfa9ef4706e2",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Contoso Company",
    "createdDateTime": "2020-10-30T21:03:00.0000000Z",
    "updatedDateTime": "2020-10-30T21:03:00.0000000Z",
    "status": "New",
    "substatus": "Pending",
    "qualification": "Direct",
    "type": "Independent",
    "direction": "Incoming",
    "customerProfile": {
      "name": "Fabrikam Customer Inc",
      "address": {
        "addressLine1": "One Microsoft Way",
        "addressLine2": "",
        "city": "Redmond",
        "state": "WA",
        "postalCode": "98052",
        "country": "US"
      }
    },
    "details": {
      "notes": "We are interested in deploying Microsoft 365 and are looking forsupport in training our employees. Can you help?",
      "dealValue": 10000,
      "currency": "USD",
      "closingDateTime": "2020-12-01T00:00:00Z",
      "requirements": {
          "industries": [ { "id": "Education" } ],
          "products": [ { "id": "Microsoft365" } ],
          "services": [ { "id": "LearningAndCertification" } ],
          "solutions": [ { "id": "SOL-Microsoft365", "name": "Microsoft365" }
        ]
      }
    },
    "links": {
      "relatedReferrals": {
        "uri": "https://api.partner.microsoft.com/v1.0/engagements/referrals$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'",
        "method": "GET"
      },
      "self": {
        "uri": "https://api.partner.microsoft.com/v1.0/engagements/referralsc5fbb3b6-be74-4795-9fb5-4324c73fed37",
        "method": "GET"
      }
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\""
}
```

> [!Note]
> A fenti példában illustratration lévő mezők nem teljesek. A tényleges API-válasz több mezőt is tartalmaz, például az ügyfél és a partner csapatát. A támogatott mezők teljes listáját az [Ajánlói erőforrások](referral-resources.md)című részben tekintheti meg.