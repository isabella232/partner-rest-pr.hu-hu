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
# <a name="get-foreign-exchange-rates"></a><span data-ttu-id="92f58-103">Valutaátváltási árfolyamok lekérése</span><span class="sxs-lookup"><span data-stu-id="92f58-103">Get foreign exchange rates</span></span>

<span data-ttu-id="92f58-104">A következőkre vonatkozik:</span><span class="sxs-lookup"><span data-stu-id="92f58-104">Applies to:</span></span>

- <span data-ttu-id="92f58-105">Partner API</span><span class="sxs-lookup"><span data-stu-id="92f58-105">Partner API</span></span>

<span data-ttu-id="92f58-106">Ez a témakör bemutatja, hogyan szerezhet be egy adott hónapra vonatkozóan az átváltási díjakat.</span><span class="sxs-lookup"><span data-stu-id="92f58-106">This topic explains how to get foreign exchange rates for a given month.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92f58-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="92f58-107">Prerequisites</span></span>

- <span data-ttu-id="92f58-108">A [partner API-hitelesítésben](api-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="92f58-108">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="92f58-109">Ez a forgatókönyv csak az alkalmazás felhasználói hitelesítését támogatja.</span><span class="sxs-lookup"><span data-stu-id="92f58-109">This scenario only supports application user authentication.</span></span> <span data-ttu-id="92f58-110">Az Application-only még nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="92f58-110">Application-only is not yet supported.</span></span>
- <span data-ttu-id="92f58-111">Ez az API jelenleg csak a felhasználói hozzáférést támogatja, ahol a partnereknek a következő szerepkörök egyikében kell lenniük: globális rendszergazda, felügyeleti ügynök vagy értékesítési ügynök.</span><span class="sxs-lookup"><span data-stu-id="92f58-111">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Admin Agent or Sales Agent.</span></span>


## <a name="details"></a><span data-ttu-id="92f58-112">Részletek</span><span class="sxs-lookup"><span data-stu-id="92f58-112">Details</span></span>

- <span data-ttu-id="92f58-113">Jelenleg használatban van az [árlista API](get-a-price-sheet.md) -val, hogy kiszámítsa az Azure Plan CSP-beli helyi pénznemek várható díjait.</span><span class="sxs-lookup"><span data-stu-id="92f58-113">Currently used with [get price sheet API](get-a-price-sheet.md) to calculate expected charges for Azure plan CSP local currencies.</span></span>
- <span data-ttu-id="92f58-114">A devizák díjai a teljes hónapra érvényesek.</span><span class="sxs-lookup"><span data-stu-id="92f58-114">Foreign exchange rates hold true for the entire month they are posted.</span></span>
- <span data-ttu-id="92f58-115">Az Azure-csomag [díjszabásával](pricing.md) kapcsolatos további információkért tekintse meg az [Azure-csomag díjszabási dokumentációját](https://docs.microsoft.com/partner-center/azure-plan-price-list).</span><span class="sxs-lookup"><span data-stu-id="92f58-115">More information about Azure plan [pricing](pricing.md) can be found in the [Azure plan pricing documentation](https://docs.microsoft.com/partner-center/azure-plan-price-list).</span></span>
- <span data-ttu-id="92f58-116">A partneri díjszabás és a deviza-árfolyam API-k nem részei a [partner Center SDK](https://docs.microsoft.com/partner-center/develop/get-started)-nak.</span><span class="sxs-lookup"><span data-stu-id="92f58-116">Partner pricing and foreign exchange rate APIs are not part of the [Partner Center SDK](https://docs.microsoft.com/partner-center/develop/get-started).</span></span>
- <span data-ttu-id="92f58-117">Ez a metódus egy fájl streamként adja vissza az eredményeket.</span><span class="sxs-lookup"><span data-stu-id="92f58-117">This method returns results as a file stream.</span></span> <span data-ttu-id="92f58-118">A fájl stream egy. csv-fájl vagy a. csv zip tömörített verziója.</span><span class="sxs-lookup"><span data-stu-id="92f58-118">File stream is either a .csv file or a zip compressed version of the .csv.</span></span> <span data-ttu-id="92f58-119">A tömörített fájlok igénylésének részleteit alább találja.</span><span class="sxs-lookup"><span data-stu-id="92f58-119">Details about how to request compressed files are included below.</span></span>

## <a name="rest-request"></a><span data-ttu-id="92f58-120">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="92f58-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="92f58-121">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="92f58-121">Request syntax</span></span>

| <span data-ttu-id="92f58-122">Metódus</span><span class="sxs-lookup"><span data-stu-id="92f58-122">Method</span></span>   | <span data-ttu-id="92f58-123">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="92f58-123">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="92f58-124">**GET**</span><span class="sxs-lookup"><span data-stu-id="92f58-124">**GET**</span></span> | <span data-ttu-id="92f58-125"> https://api.partner.microsoft.com/v1.0/sales/fxrates(Month="{Month}")/$value</span><span class="sxs-lookup"><span data-stu-id="92f58-125">https://api.partner.microsoft.com/v1.0/sales/fxrates(Month='{month}')/$value</span></span>                                  |

### <a name="uri-required-parameters"></a><span data-ttu-id="92f58-126">URI szükséges paraméterek</span><span class="sxs-lookup"><span data-stu-id="92f58-126">URI required parameters</span></span>

<span data-ttu-id="92f58-127">A következő elérésiút-paraméterek használatával kérheti le a kívánt átváltási árfolyamok hónapját.</span><span class="sxs-lookup"><span data-stu-id="92f58-127">Use the following path parameters to request the month of foreign exchange rates you want.</span></span>

| <span data-ttu-id="92f58-128">Név</span><span class="sxs-lookup"><span data-stu-id="92f58-128">Name</span></span>                   | <span data-ttu-id="92f58-129">Típus</span><span class="sxs-lookup"><span data-stu-id="92f58-129">Type</span></span>     | <span data-ttu-id="92f58-130">Kötelező</span><span class="sxs-lookup"><span data-stu-id="92f58-130">Required</span></span> | <span data-ttu-id="92f58-131">Leírás</span><span class="sxs-lookup"><span data-stu-id="92f58-131">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="92f58-132">Month (hónap)</span><span class="sxs-lookup"><span data-stu-id="92f58-132">Month</span></span>                      | <span data-ttu-id="92f58-133">sztring</span><span class="sxs-lookup"><span data-stu-id="92f58-133">string</span></span>   | <span data-ttu-id="92f58-134">Igen</span><span class="sxs-lookup"><span data-stu-id="92f58-134">Yes</span></span>       | <span data-ttu-id="92f58-135">YYYMM formátumúnak kell lennie.</span><span class="sxs-lookup"><span data-stu-id="92f58-135">Must be in YYYMM format.</span></span> <span data-ttu-id="92f58-136">Ha az alapértelmezett érték nincs megadva az aktuális hónapban.</span><span class="sxs-lookup"><span data-stu-id="92f58-136">If omitted defaults to current month.</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="92f58-137">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="92f58-137">Request headers</span></span>

- <span data-ttu-id="92f58-138">További információért lásd: [partner Rest-fejlécek](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="92f58-138">See [Partner REST headers](headers.md) for more information.</span></span>

<span data-ttu-id="92f58-139">A fenti fejléceken kívül a fájlok lekérése tömörített sávszélesség és letöltési idő alapján is lehetséges.</span><span class="sxs-lookup"><span data-stu-id="92f58-139">In addition to the above headers, files can be retrieved as compressed reducing bandwidth and download times.</span></span> <span data-ttu-id="92f58-140">Alapértelmezés szerint a fájlok nincsenek tömörítve.</span><span class="sxs-lookup"><span data-stu-id="92f58-140">By default the files are not compressed.</span></span> <span data-ttu-id="92f58-141">A fájlok tömörített verziójának beolvasásához a következő fejlécet kell megadnia.</span><span class="sxs-lookup"><span data-stu-id="92f58-141">To get compressed versions of the files you can include the below header value.</span></span> <span data-ttu-id="92f58-142">Vegye figyelembe, hogy a tömörített lapok csak a 2020 áprilisa óta érhetők el, a 2020. április előtti összes kérelem csak nem tömörítettként érhető el.</span><span class="sxs-lookup"><span data-stu-id="92f58-142">Realize that compressed sheets are only available from April 2020 onward, all requests prior to April 2020 are only available as not compressed.</span></span>

| <span data-ttu-id="92f58-143">Fejléc</span><span class="sxs-lookup"><span data-stu-id="92f58-143">Header</span></span>                   | <span data-ttu-id="92f58-144">Érték típusa</span><span class="sxs-lookup"><span data-stu-id="92f58-144">Value Type</span></span>     | <span data-ttu-id="92f58-145">Érték</span><span class="sxs-lookup"><span data-stu-id="92f58-145">Value</span></span> | <span data-ttu-id="92f58-146">Leírás</span><span class="sxs-lookup"><span data-stu-id="92f58-146">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="92f58-147">Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="92f58-147">Accept-Encoding</span></span>| <span data-ttu-id="92f58-148">sztring</span><span class="sxs-lookup"><span data-stu-id="92f58-148">string</span></span>   | <span data-ttu-id="92f58-149">deflate</span><span class="sxs-lookup"><span data-stu-id="92f58-149">deflate</span></span>| <span data-ttu-id="92f58-150">Választható.</span><span class="sxs-lookup"><span data-stu-id="92f58-150">Optional.</span></span> <span data-ttu-id="92f58-151">Ha a kihagyott fájl adatfolyama nincs tömörítve.</span><span class="sxs-lookup"><span data-stu-id="92f58-151">If omitted file stream is not compressed.</span></span>       |

### <a name="request-example"></a><span data-ttu-id="92f58-152">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="92f58-152">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/fxrates(Month='201909')/$value HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a><span data-ttu-id="92f58-153">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="92f58-153">REST response</span></span>

<span data-ttu-id="92f58-154">Ha a művelet sikeres, ez a módszer a külső árfolyamokat adatfolyamként adja vissza.</span><span class="sxs-lookup"><span data-stu-id="92f58-154">If successful, this method returns foreign exchange rates as a file stream.</span></span> <span data-ttu-id="92f58-155">A fájl stream egy. csv-fájl vagy a. csv zip tömörített verziója.</span><span class="sxs-lookup"><span data-stu-id="92f58-155">File stream is either a .csv file or a zip compressed version of the .csv.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="92f58-156">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="92f58-156">Response success and error codes</span></span>

<span data-ttu-id="92f58-157">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="92f58-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="92f58-158">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="92f58-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="92f58-159">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="92f58-159">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="92f58-160">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="92f58-160">Response example</span></span>

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
