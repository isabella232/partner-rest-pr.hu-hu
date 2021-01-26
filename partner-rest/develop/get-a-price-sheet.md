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
# <a name="get-a-price-sheet"></a><span data-ttu-id="afe23-104">Árlista lekérése</span><span class="sxs-lookup"><span data-stu-id="afe23-104">Get a price sheet</span></span>

<span data-ttu-id="afe23-105">A következőkre vonatkozik:</span><span class="sxs-lookup"><span data-stu-id="afe23-105">Applies to:</span></span>

- <span data-ttu-id="afe23-106">Partner API</span><span class="sxs-lookup"><span data-stu-id="afe23-106">Partner API</span></span>

<span data-ttu-id="afe23-107">Ez a témakör azt ismerteti, hogyan lehet egy adott piacra és nézetre vonatkozó árlistát beolvasni.</span><span class="sxs-lookup"><span data-stu-id="afe23-107">This topic explains how to get a price sheet for a given market and view.</span></span> <span data-ttu-id="afe23-108">Ez a metódus támogatja a szűrőket a hónapok szerinti előzmények lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="afe23-108">This method supports filters to get history by month.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afe23-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="afe23-109">Prerequisites</span></span>

- <span data-ttu-id="afe23-110">A [partner API-hitelesítésben](api-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="afe23-110">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="afe23-111">Ez a forgatókönyv csak az alkalmazás felhasználói hitelesítését támogatja.</span><span class="sxs-lookup"><span data-stu-id="afe23-111">This scenario only supports application user authentication.</span></span> <span data-ttu-id="afe23-112">Az Application-ony még nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="afe23-112">Application-ony is not yet supported.</span></span>
- <span data-ttu-id="afe23-113">Ez az API jelenleg csak a felhasználói hozzáférést támogatja, ahol a partnereknek a következő szerepkörök egyikében kell lenniük: globális rendszergazda, felügyeleti ügynök vagy értékesítési ügynök.</span><span class="sxs-lookup"><span data-stu-id="afe23-113">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Admin Agent or Sales Agent.</span></span>

## <a name="details"></a><span data-ttu-id="afe23-114">Részletek</span><span class="sxs-lookup"><span data-stu-id="afe23-114">Details</span></span>

- <span data-ttu-id="afe23-115">Az aktuális adatok csak az Azure-csomag fogyasztása és a foglalási termékek esetében adnak vissza adatmennyiséget.</span><span class="sxs-lookup"><span data-stu-id="afe23-115">Current returns data only for Azure plan consumption and reservation products.</span></span>
- <span data-ttu-id="afe23-116">A jelenlegi [díjszabás](pricing.md) magában foglalja az aktuális hónapban az API meghívásának napjáig elérhető összes mérőszámot és terméket.</span><span class="sxs-lookup"><span data-stu-id="afe23-116">Current [pricing](pricing.md) includes all meters and products available during the current month to the date the API is called.</span></span> <span data-ttu-id="afe23-117">Az előző hónapokban az adott hónapban elérhető összes fogyasztásmérőt és terméket tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="afe23-117">Previous months include all meters and products available for the given month.</span></span>
- <span data-ttu-id="afe23-118">A használati díjak díjszabása csak USD-ben érhető el, a külföldi árfolyamok API-t használva számítjuk ki a helyi pénznem költségeit.</span><span class="sxs-lookup"><span data-stu-id="afe23-118">Consumption meter prices are only in USD, partners are to use the foreign exchange rates API to calculate local currency costs.</span></span>
- <span data-ttu-id="afe23-119">A fogyasztási fogyasztásmérők árai a becsült kiskereskedelmi árak.</span><span class="sxs-lookup"><span data-stu-id="afe23-119">Consumption meter prices are estimated retail prices.</span></span> <span data-ttu-id="afe23-120">A partneri kedvezmények a [partner által létrehozott krediteken](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation)keresztül érhetők el.</span><span class="sxs-lookup"><span data-stu-id="afe23-120">Partner discounts are available via [partner earned credit](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation).</span></span>
- <span data-ttu-id="afe23-121">A foglalások díjszabása tartalmazza a CSP-partneri kedvezményeket.</span><span class="sxs-lookup"><span data-stu-id="afe23-121">Reservations meter prices include the CSP partner discounts.</span></span> <span data-ttu-id="afe23-122">A foglalások becsült kiskereskedelmi árai a partner Center "díjszabási és ajánlatok" oldaláról letölthetők a megosztott szolgáltatások szolgáltatásban.</span><span class="sxs-lookup"><span data-stu-id="afe23-122">Estimated retail prices for reservations can be found in the reservations shared services downloadable from the Partner Center "Pricing and offers" page.</span></span>
- <span data-ttu-id="afe23-123">Az Azure-csomag díjszabásával kapcsolatos további információkért tekintse meg az [Azure-csomag díjszabási dokumentációját](https://docs.microsoft.com/partner-center/azure-plan-price-list).</span><span class="sxs-lookup"><span data-stu-id="afe23-123">More information about Azure plan pricing can be found in the [Azure plan pricing documentation](https://docs.microsoft.com/partner-center/azure-plan-price-list).</span></span>
- <span data-ttu-id="afe23-124">A partneri díjszabás és a deviza-árfolyam API-k nem részei a [partner Center SDK](https://docs.microsoft.com/partner-center/develop/get-started)-nak.</span><span class="sxs-lookup"><span data-stu-id="afe23-124">Partner pricing and foreign exchange rate APIs are not part of the [Partner Center SDK](https://docs.microsoft.com/partner-center/develop/get-started).</span></span>
- <span data-ttu-id="afe23-125">Ez a metódus a árlista értékét adja vissza fájl adatfolyamként.</span><span class="sxs-lookup"><span data-stu-id="afe23-125">This method returns the price list as a file stream.</span></span> <span data-ttu-id="afe23-126">A fájl stream egy. csv-fájl vagy a. csv zip tömörített verziója.</span><span class="sxs-lookup"><span data-stu-id="afe23-126">File stream is either a .csv file or a zip compressed version of the .csv.</span></span> <span data-ttu-id="afe23-127">A tömörített fájlok igénylésének részleteit alább találja.</span><span class="sxs-lookup"><span data-stu-id="afe23-127">Details about how to request compressed files are included below.</span></span>

## <a name="rest-request"></a><span data-ttu-id="afe23-128">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="afe23-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="afe23-129">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="afe23-129">Request syntax</span></span>

| <span data-ttu-id="afe23-130">Metódus</span><span class="sxs-lookup"><span data-stu-id="afe23-130">Method</span></span>   | <span data-ttu-id="afe23-131">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="afe23-131">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="afe23-132">**GET**</span><span class="sxs-lookup"><span data-stu-id="afe23-132">**GET**</span></span> | <span data-ttu-id="afe23-133"> https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market="{Market}", PricesheetView = "{View}")/$value</span><span class="sxs-lookup"><span data-stu-id="afe23-133">https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='{market}',PricesheetView='{view}')/$value</span></span>                                     |

### <a name="uri-required-parameters"></a><span data-ttu-id="afe23-134">URI szükséges paraméterek</span><span class="sxs-lookup"><span data-stu-id="afe23-134">URI required parameters</span></span>

<span data-ttu-id="afe23-135">A következő elérésiút-paraméterek használatával megadhatja, hogy melyik piacon és milyen típusú árlistát szeretne használni.</span><span class="sxs-lookup"><span data-stu-id="afe23-135">Use the following path parameters to request which market and type of price sheet you want.</span></span>

| <span data-ttu-id="afe23-136">Név</span><span class="sxs-lookup"><span data-stu-id="afe23-136">Name</span></span>                   | <span data-ttu-id="afe23-137">Típus</span><span class="sxs-lookup"><span data-stu-id="afe23-137">Type</span></span>     | <span data-ttu-id="afe23-138">Kötelező</span><span class="sxs-lookup"><span data-stu-id="afe23-138">Required</span></span> | <span data-ttu-id="afe23-139">Leírás</span><span class="sxs-lookup"><span data-stu-id="afe23-139">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="afe23-140">Piaci</span><span class="sxs-lookup"><span data-stu-id="afe23-140">Market</span></span>                      | <span data-ttu-id="afe23-141">sztring</span><span class="sxs-lookup"><span data-stu-id="afe23-141">string</span></span>   | <span data-ttu-id="afe23-142">Igen</span><span class="sxs-lookup"><span data-stu-id="afe23-142">Yes</span></span>       | <span data-ttu-id="afe23-143">Kétbetűs országkód az igényelt piacon</span><span class="sxs-lookup"><span data-stu-id="afe23-143">Two letter country code for the market being requested</span></span>       |
|<span data-ttu-id="afe23-144">PricesheetView</span><span class="sxs-lookup"><span data-stu-id="afe23-144">PricesheetView</span></span> | <span data-ttu-id="afe23-145">sztring</span><span class="sxs-lookup"><span data-stu-id="afe23-145">string</span></span>   | <span data-ttu-id="afe23-146">Igen</span><span class="sxs-lookup"><span data-stu-id="afe23-146">Yes</span></span>       | <span data-ttu-id="afe23-147">A kért árlista típusa, ez lehet azure_consumption vagy azure_reservations</span><span class="sxs-lookup"><span data-stu-id="afe23-147">The type of price sheet being requested, this can be azure_consumption or azure_reservations</span></span>       |

### <a name="uri-filter-parameters"></a><span data-ttu-id="afe23-148">URI-szűrő paramétereinek száma</span><span class="sxs-lookup"><span data-stu-id="afe23-148">URI filter parameters</span></span>

<span data-ttu-id="afe23-149">Használja a következő szűrési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="afe23-149">Use the following filter parameters.</span></span>

| <span data-ttu-id="afe23-150">Név</span><span class="sxs-lookup"><span data-stu-id="afe23-150">Name</span></span>                   | <span data-ttu-id="afe23-151">Típus</span><span class="sxs-lookup"><span data-stu-id="afe23-151">Type</span></span>     | <span data-ttu-id="afe23-152">Kötelező</span><span class="sxs-lookup"><span data-stu-id="afe23-152">Required</span></span> | <span data-ttu-id="afe23-153">Leírás</span><span class="sxs-lookup"><span data-stu-id="afe23-153">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="afe23-154">Idővonal</span><span class="sxs-lookup"><span data-stu-id="afe23-154">Timeline</span></span>| <span data-ttu-id="afe23-155">sztring</span><span class="sxs-lookup"><span data-stu-id="afe23-155">string</span></span>   | <span data-ttu-id="afe23-156">No</span><span class="sxs-lookup"><span data-stu-id="afe23-156">No</span></span>| <span data-ttu-id="afe23-157">Az alapértelmezett érték az aktuális, ha nem lett átadva.</span><span class="sxs-lookup"><span data-stu-id="afe23-157">Defaults to current if not passed.</span></span> <span data-ttu-id="afe23-158">A lehetséges értékek: előzmények, aktuális és jövőbeli.</span><span class="sxs-lookup"><span data-stu-id="afe23-158">Possible values are history, current and future.</span></span>       |
|<span data-ttu-id="afe23-159">Month (hónap)</span><span class="sxs-lookup"><span data-stu-id="afe23-159">Month</span></span>| <span data-ttu-id="afe23-160">sztring</span><span class="sxs-lookup"><span data-stu-id="afe23-160">string</span></span>   | <span data-ttu-id="afe23-161">No</span><span class="sxs-lookup"><span data-stu-id="afe23-161">No</span></span>| <span data-ttu-id="afe23-162">Csak akkor szükséges, ha az előzményeket kérik, be kell tartania a YYYYMM a kért árlista esetében.</span><span class="sxs-lookup"><span data-stu-id="afe23-162">Only required if history is requested, must adhere to YYYYMM for the price sheet being requested.</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="afe23-163">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="afe23-163">Request headers</span></span>

- <span data-ttu-id="afe23-164">További információért lásd: [partner Rest-fejlécek](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="afe23-164">See [Partner REST headers](headers.md) for more information.</span></span>

<span data-ttu-id="afe23-165">A fenti fejléceken kívül a díjszabási fájlok lekérése tömörítve csökkenti a sávszélességet és a letöltési időt.</span><span class="sxs-lookup"><span data-stu-id="afe23-165">In addition to the above headers, pricing files can be retrieved as compressed reducing bandwidth and download times.</span></span> <span data-ttu-id="afe23-166">Alapértelmezés szerint a fájlok nincsenek tömörítve.</span><span class="sxs-lookup"><span data-stu-id="afe23-166">By default the files are not compressed.</span></span> <span data-ttu-id="afe23-167">A fájlok tömörített verziójának beolvasásához a következő fejlécet kell megadnia.</span><span class="sxs-lookup"><span data-stu-id="afe23-167">To get compressed versions of the files you can include the below header value.</span></span> <span data-ttu-id="afe23-168">Vegye figyelembe, hogy a tömörített lapok csak április 2020-ig érhetők el, a 2020. április előtti összes lap csak tömörítetlen érhető el.</span><span class="sxs-lookup"><span data-stu-id="afe23-168">Realize that compressed sheets are only available from April 2020 onward, all sheets prior to April 2020 are only available as not compressed.</span></span>

| <span data-ttu-id="afe23-169">Fejléc</span><span class="sxs-lookup"><span data-stu-id="afe23-169">Header</span></span>                   | <span data-ttu-id="afe23-170">Érték típusa</span><span class="sxs-lookup"><span data-stu-id="afe23-170">Value Type</span></span>     | <span data-ttu-id="afe23-171">Érték</span><span class="sxs-lookup"><span data-stu-id="afe23-171">Value</span></span> | <span data-ttu-id="afe23-172">Leírás</span><span class="sxs-lookup"><span data-stu-id="afe23-172">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="afe23-173">Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="afe23-173">Accept-Encoding</span></span>| <span data-ttu-id="afe23-174">sztring</span><span class="sxs-lookup"><span data-stu-id="afe23-174">string</span></span>   | <span data-ttu-id="afe23-175">deflate</span><span class="sxs-lookup"><span data-stu-id="afe23-175">deflate</span></span>| <span data-ttu-id="afe23-176">Választható.</span><span class="sxs-lookup"><span data-stu-id="afe23-176">Optional.</span></span> <span data-ttu-id="afe23-177">Ha a kihagyott fájl adatfolyama nincs tömörítve.</span><span class="sxs-lookup"><span data-stu-id="afe23-177">If omitted file stream is not compressed.</span></span>       |

### <a name="request-example"></a><span data-ttu-id="afe23-178">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="afe23-178">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='ad',PricesheetView='azure_consumption')/$value?timeline=history&month=201909 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a><span data-ttu-id="afe23-179">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="afe23-179">REST response</span></span>

<span data-ttu-id="afe23-180">Ha a művelet sikeres, ez a metódus a árlista fájlként adja vissza az árlistát.</span><span class="sxs-lookup"><span data-stu-id="afe23-180">If successful, this method returns the price list as a file stream.</span></span> <span data-ttu-id="afe23-181">A fájl stream egy. csv-fájl vagy a. csv zip tömörített verziója.</span><span class="sxs-lookup"><span data-stu-id="afe23-181">File stream is either a .csv file or a zip compressed version of the .csv.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="afe23-182">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="afe23-182">Response success and error codes</span></span>

<span data-ttu-id="afe23-183">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="afe23-183">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="afe23-184">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="afe23-184">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="afe23-185">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="afe23-185">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="afe23-186">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="afe23-186">Response example</span></span>

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
