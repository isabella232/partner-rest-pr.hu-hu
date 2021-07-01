---
title: Árlista lekérése
description: Árlap beszerzése egy adott piacról és nézetről. Támogatja a szűrőket, hogy hónap szerint lekért előzményeket kapj.
ms.date: 01/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 7571e8fce861dbfe463000a1ac4094115af08ffa
ms.sourcegitcommit: 9e64d6358ef4e1ac2d3e0d36cd63490a5f760b38
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/01/2021
ms.locfileid: "113125516"
---
# <a name="get-a-price-sheet"></a>Árlista lekérése

A következőkre vonatkozik:

- Partner API

Ez a témakör azt ismerteti, hogyan lehet árlapot lekért egy adott piachoz és nézethez. Ez a metódus támogatja a szűrőket az előzmények hónap szerint való lekérthez.

## <a name="prerequisites"></a>Előfeltételek

- Az Partner API [ismertetett hitelesítő adatok.](api-authentication.md) Ez a forgatókönyv csak az alkalmazásfelhasználói hitelesítést támogatja. A csak alkalmazás még nem támogatott. A **HTTP-hiba:400 hibát** tapasztaló partnereknek érdemes a Partner API [dokumentációjában.](api-authentication.md)
- Ez az API jelenleg csak olyan felhasználói hozzáférést támogat, ahol a partnereknek a következő szerepkörök egyikében kell részt részte): globális rendszergazda, rendszergazdai ügynök vagy értékesítési ügynök.

## <a name="details"></a>Részletek

- A Current csak az Azure-csomag felhasználási és foglalási termékeinek adatait adja vissza.
- Az [aktuális díjszabás](pricing.md) az API hívásának dátumig az aktuális hónapban elérhető összes mérőt és terméket tartalmazza. Az előző hónapokban az adott hónapban elérhető összes mérőt és terméket tartalmazzák.
- A fogyasztásmérők árai csak USD-ben vannak meg, a partnereknek a foreign exchange rates API-t kell használniuk a helyi pénznem költségeinek kiszámításához.
- A fogyasztásmérők árai a becsült kiskereskedelmi árak. A partneri kedvezmények a [partneri jóváíráson keresztül érhetők el.](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation)
- A Reservations mérőárai tartalmazzák a CSP-partneri kedvezményeket. A foglalások becsült kiskereskedelmi árai a "Díjszabás és ajánlatok" Partnerközpont letölthető foglalások megosztott szolgáltatásaiban találhatók.
- Az Azure-csomag díjszabását az [Azure-csomag díjszabási dokumentációjában találhatja meg.](https://docs.microsoft.com/partner-center/azure-plan-price-list)
- A partnerek díjszabása és a árfolyam API-k nem részei a [Partnerközpont SDK.](https://docs.microsoft.com/partner-center/develop/get-started)
- Ez a metódus fájlstreamként adja vissza az árlistát. A fájlstream egy .csv fájl vagy a fájl tömörített .csv. A tömörített fájlok lekérésének részletei az alábbiakban olvashatók.

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus   | Kérés URI-ja                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Kap** | https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='{market}',PricesheetView='{view}')/$value                                     |

### <a name="uri-required-parameters"></a>URI szükséges paraméterei

Az alábbi elérésiút-paraméterekkel kérheti le, hogy melyik piaci és árlaptípust szeretné használni.

| Név                   | Típus     | Kötelező | Leírás                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Piac                      | sztring   | Igen       | Kétbetűs országkód a kért piachoz       |
|PricesheetView | sztring   | Igen       | A kért árlap típusa, amely nem azure_consumption, azure_reservations frissíthető.  |

> [!Note]
> A updatedlicensebased PriceSheetView jelenleg csak olyan partnerek számára érhető el, akik az M365/D365 új kereskedelmi felhasználói élmény technikai előzetes kiadásának részei.

### <a name="uri-filter-parameters"></a>URI-szűrőparaméterek

Használja az alábbi szűrőparamétereket.

| Név                   | Típus     | Kötelező | Leírás                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Idővonal| sztring   | No| Az alapértelmezett érték az aktuális, ha nem ad át értéket. Lehetséges értékek: előzmények, aktuális és jövőbeli.       |
|Month (hónap)| sztring   | No| Csak akkor szükséges, ha az előzmények lekérése meg van kérve, meg kell felelnie az YYYYMM értéknek a kért árlaphoz.       |

### <a name="request-headers"></a>Kérésfejlécek

- További [információ: Partner REST-fejlécek.](headers.md)

A fenti fejlécek mellett a díjszabási fájlok tömörített sávszélesség-csökkentő és letöltési időként is lekért fájlokként olvashatók be. Alapértelmezés szerint a fájlok nincsenek tömörítve. A fájlok tömörített verzióit az alábbi fejlécértékkel kaphatja meg. Ne feledni, hogy a tömörített lapok csak 2020 áprilisától érhetők el, a 2020 áprilisa előtti lapok csak nem tömörítettként érhetők el.

| Fejléc                   | Érték típusa     | Érték | Leírás                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Accept-Encoding| sztring   | Deflate| Választható. Ha nincs megadva, a fájlstream nem tömörített.       |

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='ad',PricesheetView='azure_consumption')/$value?timeline=history&month=201909 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```
### <a name="request-example-for-new-commerce"></a>Példa kérése új kereskedelemhez

> [!Note]
> A updatedlicensebased PriceSheetView jelenleg csak olyan partnerek számára érhető el, akik az M365/D365 új kereskedelmi felhasználói élmény technikai előzetes kiadásának részei.

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='US',PricesheetView='updatedlicensebased')/$value?timeline=history&month=202101 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, ez a metódus fájlstreamként adja vissza az árlistát. A fájlstream egy .csv fájl vagy a fájl tömörített .csv.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

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

### <a name="response-example-for-new-commerce"></a>Válasz példa új kereskedelemre

> [!Note]
> A updatedlicensebased PriceSheetView jelenleg csak olyan partnerek számára érhető el, akik az M365/D365 új kereskedelmi felhasználói élmény technikai előzetes kiadásának részei.

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 42180180
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=sheets.csv
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
Date: Wed, 02 Feb 2021 03:41:20 GMT

"ProductTitle","ProductId","SkuId","SkuTitle","Publisher","SkuDescription","UnitOfMeasure","TermDuration","BillingPlan","Market","Currency","UnitPrice","PricingTierRangeMin","PricingTierRangeMax","EffectiveStartDate","EffectiveEndDate","Tags","ERP Price“
"Advanced Communications","CFQ7TTC0HDK0","0001","Advanced Communications","Microsoft Corporation","Advanced meetings, calling, workflow integration, and management tools for IT.","","P1Y","Annual","US","USD","115.2","","","2/1/2019 12:00:00 AM","2/4/2021 8:35:31 PM","License","144"
======= Truncated ==============

```
