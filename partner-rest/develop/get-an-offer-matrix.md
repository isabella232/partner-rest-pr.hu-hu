---
title: Ajánlatmátrix lekérte
description: Szerezzen be egy ajánlatmátrixot egy adott dátumhoz. Támogatja a szűrőket, hogy hónap szerint lekért előzményeket kap.
ms.date: 02/11/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: e53276c1170febab002d35a42c88c1f96f7b7428
ms.sourcegitcommit: 9e64d6358ef4e1ac2d3e0d36cd63490a5f760b38
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/01/2021
ms.locfileid: "113131300"
---
# <a name="get-an-offer-matrix"></a>Ajánlatmátrix lekérte

A következőkre vonatkozik:

- Partner API
- Az M365/D365 Új kereskedelmi élmény technikai előzetes verziója. Az alábbi új kereskedelmi változások jelenleg csak az M365/D365 új kereskedelmi felhasználói élményének technikai előzetesében részt vesző partnerek számára érhetők el.

Ez a témakör azt ismerteti, hogyan lehet lekért ajánlatmátrixot egy adott hónapra. Az ajánlat mátrixa tulajdonságokat és vásárlási szabályokat tartalmaz a termékekhez és a terméktermékekhez. Ez a metódus támogatja a szűrőket az előzmények havi lekért lekérthez.

## <a name="prerequisites"></a>Előfeltételek

- Az Partner API [ismertetett hitelesítő adatok.](api-authentication.md) Ez a forgatókönyv csak az alkalmazásfelhasználói hitelesítést támogatja. A csak alkalmazás még nem támogatott. A **HTTP-hibát:400 tapasztaló** partnereknek érdemes a Partner API [dokumentációját.](api-authentication.md)
- Ez az API jelenleg csak olyan felhasználói hozzáférést támogat, ahol a partnereknek a következő szerepkörök egyikében kell részt részte): globális rendszergazda, rendszergazdai ügynök vagy értékesítési ügynök.

## <a name="details"></a>Részletek

- A Current csak a frissített új kereskedelmi licencalapú termékek adatait adja vissza.
- Az aktuális díjszabás az API hívásának dátumig az aktuális hónapban elérhető termékeket tartalmazza. Az előző hónapok tartalmazzák a kiválasztott hónap utolsó napját.
- Ez a metódus fájlstreamként ad vissza adatokat. A fájlstream egy .csv fájl vagy a fájl tömörített .csv. A tömörített fájlok lekérésének részletei az alábbiakban olvashatók.

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus   | Kérés URI-ja                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Kap** | https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month="{date}")/$value |

### <a name="uri-filter-parameters"></a>URI-szűrőparaméterek

Használja az alábbi szűrőparamétereket.

| Név                   | Típus     | Kötelező | Leírás                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Month (hónap)| sztring   | No | Meg kell felelnie az YYYYMM értéknek a kért árlaphoz. |

### <a name="request-headers"></a>Kérésfejlécek

- További [információ: Partner REST-fejlécek.](headers.md)

A fenti fejlécek mellett a díjszabási fájlok tömörített sávszélesség-csökkentő és letöltési időként is lekért fájlokként olvashatók be. Alapértelmezés szerint a fájlok nincsenek tömörítve. A fájlok tömörített verzióit az alábbi fejlécértékkel kaphatja meg. Ne feledni, hogy a tömörített lapok csak 2020 áprilisától érhetők el, a 2020 áprilisa előtti lapok csak nem tömörítettként érhetők el.

| Fejléc                   | Érték típusa     | Érték | Leírás                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Accept-Encoding| sztring   | Deflate| Választható. Ha nincs megadva, a fájlstream nem tömörített.       |

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month='202101')/$value HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, ez a metódus egy ajánlatmátrixot ad vissza fájlstreamként. A fájlstream egy .csv fájl vagy a fájl tömörített .csv.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 42180180
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=updatedoffice.csv
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
Date: Wed, 02 Feb 2021 03:41:20 GMT

"ProductTitle","ProductId","SkuId","SkuTitle","ProvisioningId","ProvisioningString","MinLicenses","MaxLicenses","AssetOwnershipLimit","AssetOwnershipLimitType","ProductSkuPreRequisites","ProductSkuConversion","Description","AllowedCountries" 
"Microsoft 365 Business Basic","CFQ7TTC0LH18","0001","Microsoft 365 Business Basic","3b555118-da6a-4418-894f-7df1e2096870","O365_BUSINESS_ESSENTIALS","1","300","2","ConcurrentCount","","CFQ7TTC0LDPB/0001,CFQ7TTC0LF8Q/0001","Best for businesses that need professional...","AD;AE;AF;AG;AI;AL;AM;AO..."
======= Truncated ==============

```
