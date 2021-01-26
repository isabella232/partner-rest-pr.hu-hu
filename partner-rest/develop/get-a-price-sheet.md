---
title: Árlista lekérése
description: Egy adott piacra és nézetre vonatkozó árlista beszerzése. A támogatja a szűrőket a hónapok szerinti előzmények lekéréséhez.
ms.date: 01/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 5195ebed6559bd71a7832a667e63ee801be1c82f
ms.sourcegitcommit: bb3f5f7ee0489bded86fe52e55018c1f4f5032e2
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/07/2020
ms.locfileid: "97770518"
---
# <a name="get-a-price-sheet"></a>Árlista lekérése

A következőkre vonatkozik:

- Partner API

Ez a témakör azt ismerteti, hogyan lehet egy adott piacra és nézetre vonatkozó árlistát beolvasni. Ez a metódus támogatja a szűrőket a hónapok szerinti előzmények lekéréséhez.

## <a name="prerequisites"></a>Előfeltételek

- A [partner API-hitelesítésben](api-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak az alkalmazás felhasználói hitelesítését támogatja. Az Application-ony még nem támogatott.
- Ez az API jelenleg csak a felhasználói hozzáférést támogatja, ahol a partnereknek a következő szerepkörök egyikében kell lenniük: globális rendszergazda, felügyeleti ügynök vagy értékesítési ügynök.

## <a name="details"></a>Részletek

- Az aktuális adatok csak az Azure-csomag fogyasztása és a foglalási termékek esetében adnak vissza adatmennyiséget.
- A jelenlegi [díjszabás](pricing.md) magában foglalja az aktuális hónapban az API meghívásának napjáig elérhető összes mérőszámot és terméket. Az előző hónapokban az adott hónapban elérhető összes fogyasztásmérőt és terméket tartalmazza.
- A használati díjak díjszabása csak USD-ben érhető el, a külföldi árfolyamok API-t használva számítjuk ki a helyi pénznem költségeit.
- A fogyasztási fogyasztásmérők árai a becsült kiskereskedelmi árak. A partneri kedvezmények a [partner által létrehozott krediteken](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation)keresztül érhetők el.
- A foglalások díjszabása tartalmazza a CSP-partneri kedvezményeket. A foglalások becsült kiskereskedelmi árai a partner Center "díjszabási és ajánlatok" oldaláról letölthetők a megosztott szolgáltatások szolgáltatásban.
- Az Azure-csomag díjszabásával kapcsolatos további információkért tekintse meg az [Azure-csomag díjszabási dokumentációját](https://docs.microsoft.com/partner-center/azure-plan-price-list).
- A partneri díjszabás és a deviza-árfolyam API-k nem részei a [partner Center SDK](https://docs.microsoft.com/partner-center/develop/get-started)-nak.
- Ez a metódus a árlista értékét adja vissza fájl adatfolyamként. A fájl stream egy. csv-fájl vagy a. csv zip tömörített verziója. A tömörített fájlok igénylésének részleteit alább találja.

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus   | Kérés URI-ja                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **GET** | https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market="{Market}", PricesheetView = "{View}")/$value                                     |

### <a name="uri-required-parameters"></a>URI szükséges paraméterek

A következő elérésiút-paraméterek használatával megadhatja, hogy melyik piacon és milyen típusú árlistát szeretne használni.

| Név                   | Típus     | Kötelező | Leírás                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Piaci                      | sztring   | Igen       | Kétbetűs országkód az igényelt piacon       |
|PricesheetView | sztring   | Igen       | A kért árlista típusa, ez lehet azure_consumption vagy azure_reservations       |

### <a name="uri-filter-parameters"></a>URI-szűrő paramétereinek száma

Használja a következő szűrési paramétereket.

| Név                   | Típus     | Kötelező | Leírás                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Idővonal| sztring   | No| Az alapértelmezett érték az aktuális, ha nem lett átadva. A lehetséges értékek: előzmények, aktuális és jövőbeli.       |
|Month (hónap)| sztring   | No| Csak akkor szükséges, ha az előzményeket kérik, be kell tartania a YYYYMM a kért árlista esetében.       |

### <a name="request-headers"></a>Kérésfejlécek

- További információért lásd: [partner Rest-fejlécek](headers.md) .

A fenti fejléceken kívül a díjszabási fájlok lekérése tömörítve csökkenti a sávszélességet és a letöltési időt. Alapértelmezés szerint a fájlok nincsenek tömörítve. A fájlok tömörített verziójának beolvasásához a következő fejlécet kell megadnia. Vegye figyelembe, hogy a tömörített lapok csak április 2020-ig érhetők el, a 2020. április előtti összes lap csak tömörítetlen érhető el.

| Fejléc                   | Érték típusa     | Érték | Leírás                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Accept-Encoding| sztring   | deflate| Választható. Ha a kihagyott fájl adatfolyama nincs tömörítve.       |

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='ad',PricesheetView='azure_consumption')/$value?timeline=history&month=201909 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, ez a metódus a árlista fájlként adja vissza az árlistát. A fájl stream egy. csv-fájl vagy a. csv zip tömörített verziója.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát lásd: [hibakódok](error-codes.md).

### <a name="response-example"></a>Példa válaszra

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 42180180
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=pricesheet
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
Date: Wed, 02 Oct 2019 03:41:20 GMT

"ProductTitle","ProductId","SkuId","SkuTitle","Publisher","SkuDescription","UnitOfMeasure","TermDuration","Market","Currency","UnitPrice","PricingTierRangeMin","PricingTierRangeMax","EffectiveStartDate","EffectiveEndDate","MeterIds","MeterType","Tags“
"Advanced Data Security - SQL Database","DZH318Z0C16V","001J","Advanced Data Security - SQL Database - Standard - US East 2","Microsoft","Advanced Data Security - SQL Database - Standard - US East 2","1 Node/Month","payG-1","US","USD","15","","","3/1/2018 12:00:00 AM","11/30/9999 11:59:59 PM","cb0969aa-aaaa-4d6c-ab4b-7e182fa06aff","1 Node/Month","Azure“
======= Truncated ==============

```
