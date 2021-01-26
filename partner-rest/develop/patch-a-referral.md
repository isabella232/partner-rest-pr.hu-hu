---
title: Érdeklődő vagy lehetőség frissítése
description: Lehetővé teszi az érdeklődő vagy a lehetőség részleteinek frissítését.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: abfe7308f46cd65b9358b369f6fa05bcca4c1df2
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770542"
---
# <a name="update-a-lead-or-opportunity"></a>Érdeklődő vagy lehetőség frissítése

A következőkre vonatkozik:

- Partner API

Ez a témakör azt ismerteti, hogyan frissítheti az érdeklődők vagy a lehetőségek részleteit, például az ügylet értékét, a becsült zárási dátumot, illetve az értékesítési fázisok kezelését a további részletek között.

## <a name="prerequisites"></a>Előfeltételek

- A [partner API-hitelesítésben](api-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az App + User hitelesítő adataival.
- Ez az API jelenleg csak a felhasználói hozzáférést támogatja, ahol a partnereknek a következő szerepkörök egyikében kell lenniük: globális rendszergazda, hivatkozó rendszergazda vagy hivatkozó felhasználó.

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                       |
|---------|-------------------------------------------------------------------|
| **JAVÍTÁS** | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}> |

### <a name="uri-parameter"></a>URI-paraméter


| Név                   | Típus     | Kötelező | Leírás                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Id                      | sztring   | Igen       | Az érdeklődő vagy a közös értékesítés lehetőség egyedi azonosítója       |

### <a name="request-headers"></a>Kérésfejlécek

További információért lásd: [partner Rest-fejlécek](headers.md) .

### <a name="request-body"></a>A kérés törzse

A kérelem törzse a [JSON-javító](https://tools.ietf.org/html/rfc6902) formátumot követi. A JSON-javítási dokumentumok tömbje műveletekből áll. Minden művelet egy adott típusú változást azonosít. Ilyen változások például egy tömb elem hozzáadása vagy egy tulajdonságérték cseréje.

> [!Important]
> Az API jelenleg csak a `replace` és a `add` műveleteket támogatja.

### <a name="request-example"></a>Példa kérésre

```http
PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
Authorization: Bearer <token>
Content-Type: application/json
Prefer: return=representation

[
    {
        "op": "replace",
        "path": "/details/dealValue",
        "value": "10000"
    },
    {
        "op": "add",
        "path": "/team/-",
        "value": {
            "email": "jane.doe@contoso.com",
            "firstName": "Jane",
            "lastName": "Doe",
            "phoneNumber": "0000000001"
        }
    }
]
```

> [!Note]
> Ha a rendszer átadja az **IF-Match** fejlécet, a rendszer a Egyidejűség vezérlésére használja.

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, a válasz törzse tartalmazza a frissített [érdeklődőt vagy lehetőséget](referral-resources.md).


### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy [http-állapotkód](error-codes.md) , amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek beolvasásához használjon hálózati nyomkövetési eszközt.

### <a name="response-example"></a>Példa válaszra

``` http
HTTP/1.1 204 No Content
Content-Length: 0
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
```

> [!Tip]
> A válasz törzse a **preferált** fejléctől függ. Ha a fejléc értéke nincs megadva a kérelemben, a válasz törzse üres, és a 204-es HTTP-állapotkód szerepel. Adja hozzá a `Prefer: return=representation` fejlécet a frissített érdeklődő vagy lehetőség beszerzéséhez.

## <a name="sample-requests"></a>Példák a kérelmekre

1. Frissíti az ügylet értékét a lehetőség 10000-re, és frissíti a megjegyzéseket. A fejléc absense miatt nincs egyidejűségi ellenőrzés `If-Match` .
    
    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    
    [
        {"op":"replace","path":"/details/dealValue","value":"10000"},
        {"op":"replace","path":"/details/notes","value":"Lorem ipsum dolor sit amet."}
    ]
    ```

2. Egy érdeklődő vagy egy megnyert lehetőség állapotát frissíti.
    
    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    
    [
        {"op":"replace", "path":"/status", "value":"Closed"},
        {"op":"replace", "path":"/substatus", "value":"Won"}
    ]
    ```

    > [!Important]
    > A `status` és a `substatus` mezőnek meg kell felelnie az [itt](referral-resources.md)leírtak szerinti átmeneti értékek megengedett készletének.

3. Új tagot ad hozzá a szervezethez az érdeklődő vagy a lehetőség csapatához. A válasz a fejléc jelenléte miatt a frissített érdeklődőt vagy lehetőséget fogja tartalmazni `Prefer: return=representation` .

    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    Prefer: return=representation
    
    [
        {
            "op": "add",
            "path": "/team/-",
            "value": {
                "email": "jane.doe@contoso.com",
                "firstName": "Jane",
                "lastName": "Doe",
                "phoneNumber": "0000000001"
            }
        }
    ]
    ```
