---
title: Érdeklődők és lehetőségek listájának beolvasása
description: Érdeklődők és lehetőségek listájának beszerzése a partner API használatával.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 46243f8484a8068827e24e1d03f39ffddade1dbf
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770530"
---
# <a name="get-the-list-of-leads-and-opportunities"></a>Érdeklődők és lehetőségek listájának lekérése

A következőkre vonatkozik:

- Partner API

 Ez a témakör bemutatja, hogyan kérheti le a Microsoft-megoldások szolgáltatójának oldaláról érkező érdeklődők listáját, és a Microsoft-értékesítők vagy más partnerek által fogadott közös értékesítési lehetőségeket. Ez a művelet a szervezet által létrehozott közös értékesítési lehetőségek vagy folyamat-ajánlatok listáját is beolvassa.

> [!Note]
> A Microsoft kereskedelmi piactérről (Azure Marketplace és AppSource) kapott érdeklődők nem támogatottak.

## <a name="prerequisites"></a>Előfeltételek

- A [partner API-hitelesítésben](api-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az App + User hitelesítő adataival.
- Ez az API jelenleg csak a felhasználói hozzáférést támogatja, ahol a partnereknek a következő szerepkörök egyikében kell lenniük: globális rendszergazda, hivatkozó rendszergazda vagy hivatkozó felhasználó.

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                    |
|:--------|:---------------------------------------------------------------|
| **GET** | <https://api.partner.microsoft.com/v1.0/engagements/referrals> |

#### <a name="supported-odata-operations"></a>Támogatott OData-műveletek

| Név     | Leírás     | Kötelező    | Példa                                                                                                                                                                                                                                                     |
|:---------|:----------------|:------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| $select  | Mezők kiválasztása  | Nem          | `/referrals?$select=id,status,customerProfile`                                                                                                                                                                                                              |
| $filter  | Szűrők eredményei | Ajánlott | `/referrals?$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'` <br/> `/referrals?$filter=status eq 'New' and qualification eq 'SalesQualified'` <br/> `/referrals?$filter=customerProfile/address/country eq 'US' and direction eq 'Incoming'` |
| $orderby | Megrendelések eredményei  | Ajánlott | `/referrals?$orderby=createdDateTime desc`                                                                                                                                                                                                                  |

#### <a name="supported-orderby-parameters"></a>Támogatott OrderBy paraméterek

A következő $orderby paraméterekkel rendezheti az érdeklődők és a lehetőségek listáját

| Név            | Típus     | Leírás                                       |
|:----------------|:---------|:--------------------------------------------------|
| createdDateTime | DateTime | Az érdeklődő vagy a lehetőség létrehozásának dátuma és időpontja |
| updatedDateTime | DateTime | Az érdeklődő vagy a lehetőség dátumának és idejének frissítése   |

### <a name="request-headers"></a>Kérésfejlécek

További információért lásd: [partner Rest-fejlécek](headers.md) .

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$orderby=createdDateTime desc HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, a válasz törzse [érdeklődőket és/vagy lehetőségeket](referral-resources.md)tartalmazó gyűjteményt tartalmaz.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy [http-állapotkód](error-codes.md) , amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek beolvasásához használjon hálózati nyomkövetési eszközt.

### <a name="response-example"></a>Példa válaszra

``` http
HTTP/1.1 200 OK
Content-Type: application/json
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731

{
  "@odata.context": "http://api.partner.microsoft.com/v1.0/$metadata#Referrals",
  "@odata.count": 1,
  "value": [
    {
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
        "notes": "We are interested in deploying Microsoft 365 and are looking for support in training our employees. Can you help?",
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
          "uri": "https://api.partner.microsoft.com/v1.0/engagements/referrals?$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'",
          "method": "GET"
        },
        "self": {
          "uri": "https://api.partner.microsoft.com/v1.0/engagements/referrals/c5fbb3b6-be74-4795-9fb5-4324c73fed37",
          "method": "GET"
        }
      }
    }
  ],
  "@odata.nextLink": "http://api.partner.microsoft.com/v1.0/referrals?$skiptoken=k181pEdP0ykypkieJfcxX"
}
```

Az `@odata.nextLink` eredmények következő oldalának beszerzéséhez használja a t.

> [!Note]
> A fenti példában illustratration lévő mezők nem teljesek. A tényleges API-válasz több mezőt is tartalmaz, például az ügyfél és a partner csapatát. A támogatott mezők teljes listáját az [Ajánlói erőforrások](referral-resources.md)című részben tekintheti meg.

## <a name="sample-requests"></a>Példák a kérelmekre

1. Az első 10 legutóbbi bejövő közös értékesítési lehetőség beolvasása. A kérelem beolvassa a Microsoft értékesítési képviselő vagy egy másik partner által kezdeményezett lehetőségeket, meghívja a szervezetet, hogy részt vegyen a közös értékesítési tevékenységben.
    
    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$top=10&$filter=(type eq 'Shared' and direction eq 'Incoming')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```

2. Beolvassa a legutóbbi bejövő érdeklődőket és lehetőségeket, amelyeket nem válaszolt.  

    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$top=10&$filter=(direction eq 'Incoming' and substatus eq 'Pending')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```

    > [!Important]
    > Ha nem válaszol egy érdeklődőre vagy lehetőségre a megadott időn belül (jelenleg 14 nap), archiváljuk a lejárt módon, és értesítjük a Microsoftot vagy a partnert, aki ezt a lehetőséget elküldte.

3. Beolvassa a szervezete által kezdeményezett legutóbbi aktív közös értékesítési lehetőségeket, amelyeket egy adott értékesítő dolgoz fel.
    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$filter=status eq 'Active' and direction eq 'Outgoing' and type eq 'Shared' and team/any(t:t/email eq 'r2d2@contoso.com')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```