---
title: Valutaátváltási árfolyamok lekérése
description: Egy adott hónapra vonatkozó árfolyamok beszerzése.
ms.date: 01/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 1e718624db54dcc2ed2b5d2d93dfd1cef0e6f96f
ms.sourcegitcommit: bb3f5f7ee0489bded86fe52e55018c1f4f5032e2
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/07/2020
ms.locfileid: "97770519"
---
# <a name="get-foreign-exchange-rates"></a>Valutaátváltási árfolyamok lekérése

A következőkre vonatkozik:

- Partner API

Ez a témakör bemutatja, hogyan szerezhet be egy adott hónapra vonatkozóan az átváltási díjakat.

## <a name="prerequisites"></a>Előfeltételek

- A [partner API-hitelesítésben](api-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak az alkalmazás felhasználói hitelesítését támogatja. Az Application-only még nem támogatott.
- Ez az API jelenleg csak a felhasználói hozzáférést támogatja, ahol a partnereknek a következő szerepkörök egyikében kell lenniük: globális rendszergazda, felügyeleti ügynök vagy értékesítési ügynök.


## <a name="details"></a>Részletek

- Jelenleg használatban van az [árlista API](get-a-price-sheet.md) -val, hogy kiszámítsa az Azure Plan CSP-beli helyi pénznemek várható díjait.
- A devizák díjai a teljes hónapra érvényesek.
- Az Azure-csomag [díjszabásával](pricing.md) kapcsolatos további információkért tekintse meg az [Azure-csomag díjszabási dokumentációját](https://docs.microsoft.com/partner-center/azure-plan-price-list).
- A partneri díjszabás és a deviza-árfolyam API-k nem részei a [partner Center SDK](https://docs.microsoft.com/partner-center/develop/get-started)-nak.
- Ez a metódus egy fájl streamként adja vissza az eredményeket. A fájl stream egy. csv-fájl vagy a. csv zip tömörített verziója. A tömörített fájlok igénylésének részleteit alább találja.

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus   | Kérés URI-ja                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **GET** | https://api.partner.microsoft.com/v1.0/sales/fxrates(Month="{Month}")/$value                                  |

### <a name="uri-required-parameters"></a>URI szükséges paraméterek

A következő elérésiút-paraméterek használatával kérheti le a kívánt átváltási árfolyamok hónapját.

| Név                   | Típus     | Kötelező | Leírás                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Month (hónap)                      | sztring   | Igen       | YYYMM formátumúnak kell lennie. Ha az alapértelmezett érték nincs megadva az aktuális hónapban.       |

### <a name="request-headers"></a>Kérésfejlécek

- További információért lásd: [partner Rest-fejlécek](headers.md) .

A fenti fejléceken kívül a fájlok lekérése tömörített sávszélesség és letöltési idő alapján is lehetséges. Alapértelmezés szerint a fájlok nincsenek tömörítve. A fájlok tömörített verziójának beolvasásához a következő fejlécet kell megadnia. Vegye figyelembe, hogy a tömörített lapok csak a 2020 áprilisa óta érhetők el, a 2020. április előtti összes kérelem csak nem tömörítettként érhető el.

| Fejléc                   | Érték típusa     | Érték | Leírás                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Accept-Encoding| sztring   | deflate| Választható. Ha a kihagyott fájl adatfolyama nincs tömörítve.       |

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partner.microsoft.com/v1.0/sales/fxrates(Month='201909')/$value HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, ez a módszer a külső árfolyamokat adatfolyamként adja vissza. A fájl stream egy. csv-fájl vagy a. csv zip tömörített verziója.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát lásd: [hibakódok](error-codes.md).

### <a name="response-example"></a>Példa válaszra

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 18548
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=fxrates
Request-ID: 65fb6e59-051b-42f7-8771-c8c139b3c901
Date: Wed, 02 Oct 2019 03:42:54 GMT

"CurrencyCode","USDPerUnit","Month"
"AED","0.27224589249009701","2019”
======= Truncated ==============

```
