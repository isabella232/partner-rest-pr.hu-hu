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
# <a name="get-a-price-sheet"></a><span data-ttu-id="8c3ae-104">Árlista lekérése</span><span class="sxs-lookup"><span data-stu-id="8c3ae-104">Get a price sheet</span></span>

<span data-ttu-id="8c3ae-105">A következőkre vonatkozik:</span><span class="sxs-lookup"><span data-stu-id="8c3ae-105">Applies to:</span></span>

- <span data-ttu-id="8c3ae-106">Partner API</span><span class="sxs-lookup"><span data-stu-id="8c3ae-106">Partner API</span></span>

<span data-ttu-id="8c3ae-107">Ez a témakör azt ismerteti, hogyan lehet árlapot lekért egy adott piachoz és nézethez.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-107">This topic explains how to get a price sheet for a given market and view.</span></span> <span data-ttu-id="8c3ae-108">Ez a metódus támogatja a szűrőket az előzmények hónap szerint való lekérthez.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-108">This method supports filters to get history by month.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c3ae-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="8c3ae-109">Prerequisites</span></span>

- <span data-ttu-id="8c3ae-110">Az Partner API [ismertetett hitelesítő adatok.](api-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="8c3ae-110">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="8c3ae-111">Ez a forgatókönyv csak az alkalmazásfelhasználói hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-111">This scenario only supports application user authentication.</span></span> <span data-ttu-id="8c3ae-112">A csak alkalmazás még nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-112">Application-only is not yet supported.</span></span> <span data-ttu-id="8c3ae-113">A **HTTP-hiba:400 hibát** tapasztaló partnereknek érdemes a Partner API [dokumentációjában.](api-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="8c3ae-113">Partners that experience **http error:400** should consult the [Partner API authentication](api-authentication.md) documentation.</span></span>
- <span data-ttu-id="8c3ae-114">Ez az API jelenleg csak olyan felhasználói hozzáférést támogat, ahol a partnereknek a következő szerepkörök egyikében kell részt részte): globális rendszergazda, rendszergazdai ügynök vagy értékesítési ügynök.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-114">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Admin Agent or Sales Agent.</span></span>

## <a name="details"></a><span data-ttu-id="8c3ae-115">Részletek</span><span class="sxs-lookup"><span data-stu-id="8c3ae-115">Details</span></span>

- <span data-ttu-id="8c3ae-116">A Current csak az Azure-csomag felhasználási és foglalási termékeinek adatait adja vissza.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-116">Current returns data only for Azure plan consumption and reservation products.</span></span>
- <span data-ttu-id="8c3ae-117">Az [aktuális díjszabás](pricing.md) az API hívásának dátumig az aktuális hónapban elérhető összes mérőt és terméket tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-117">Current [pricing](pricing.md) includes all meters and products available during the current month to the date the API is called.</span></span> <span data-ttu-id="8c3ae-118">Az előző hónapokban az adott hónapban elérhető összes mérőt és terméket tartalmazzák.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-118">Previous months include all meters and products available for the given month.</span></span>
- <span data-ttu-id="8c3ae-119">A fogyasztásmérők árai csak USD-ben vannak meg, a partnereknek a foreign exchange rates API-t kell használniuk a helyi pénznem költségeinek kiszámításához.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-119">Consumption meter prices are only in USD, partners are to use the foreign exchange rates API to calculate local currency costs.</span></span>
- <span data-ttu-id="8c3ae-120">A fogyasztásmérők árai a becsült kiskereskedelmi árak.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-120">Consumption meter prices are estimated retail prices.</span></span> <span data-ttu-id="8c3ae-121">A partneri kedvezmények a [partneri jóváíráson keresztül érhetők el.](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation)</span><span class="sxs-lookup"><span data-stu-id="8c3ae-121">Partner discounts are available via [partner earned credit](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation).</span></span>
- <span data-ttu-id="8c3ae-122">A Reservations mérőárai tartalmazzák a CSP-partneri kedvezményeket.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-122">Reservations meter prices include the CSP partner discounts.</span></span> <span data-ttu-id="8c3ae-123">A foglalások becsült kiskereskedelmi árai a "Díjszabás és ajánlatok" Partnerközpont letölthető foglalások megosztott szolgáltatásaiban találhatók.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-123">Estimated retail prices for reservations can be found in the reservations shared services downloadable from the Partner Center "Pricing and offers" page.</span></span>
- <span data-ttu-id="8c3ae-124">Az Azure-csomag díjszabását az [Azure-csomag díjszabási dokumentációjában találhatja meg.](https://docs.microsoft.com/partner-center/azure-plan-price-list)</span><span class="sxs-lookup"><span data-stu-id="8c3ae-124">More information about Azure plan pricing can be found in the [Azure plan pricing documentation](https://docs.microsoft.com/partner-center/azure-plan-price-list).</span></span>
- <span data-ttu-id="8c3ae-125">A partnerek díjszabása és a árfolyam API-k nem részei a [Partnerközpont SDK.](https://docs.microsoft.com/partner-center/develop/get-started)</span><span class="sxs-lookup"><span data-stu-id="8c3ae-125">Partner pricing and foreign exchange rate APIs are not part of the [Partner Center SDK](https://docs.microsoft.com/partner-center/develop/get-started).</span></span>
- <span data-ttu-id="8c3ae-126">Ez a metódus fájlstreamként adja vissza az árlistát.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-126">This method returns the price list as a file stream.</span></span> <span data-ttu-id="8c3ae-127">A fájlstream egy .csv fájl vagy a fájl tömörített .csv.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-127">File stream is either a .csv file or a zip compressed version of the .csv.</span></span> <span data-ttu-id="8c3ae-128">A tömörített fájlok lekérésének részletei az alábbiakban olvashatók.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-128">Details about how to request compressed files are included below.</span></span>

## <a name="rest-request"></a><span data-ttu-id="8c3ae-129">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="8c3ae-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8c3ae-130">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="8c3ae-130">Request syntax</span></span>

| <span data-ttu-id="8c3ae-131">Metódus</span><span class="sxs-lookup"><span data-stu-id="8c3ae-131">Method</span></span>   | <span data-ttu-id="8c3ae-132">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="8c3ae-132">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8c3ae-133">**Kap**</span><span class="sxs-lookup"><span data-stu-id="8c3ae-133">**GET**</span></span> | <span data-ttu-id="8c3ae-134"> https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='{market}',PricesheetView='{view}')/$value</span><span class="sxs-lookup"><span data-stu-id="8c3ae-134">https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='{market}',PricesheetView='{view}')/$value</span></span>                                     |

### <a name="uri-required-parameters"></a><span data-ttu-id="8c3ae-135">URI szükséges paraméterei</span><span class="sxs-lookup"><span data-stu-id="8c3ae-135">URI required parameters</span></span>

<span data-ttu-id="8c3ae-136">Az alábbi elérésiút-paraméterekkel kérheti le, hogy melyik piaci és árlaptípust szeretné használni.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-136">Use the following path parameters to request which market and type of price sheet you want.</span></span>

| <span data-ttu-id="8c3ae-137">Név</span><span class="sxs-lookup"><span data-stu-id="8c3ae-137">Name</span></span>                   | <span data-ttu-id="8c3ae-138">Típus</span><span class="sxs-lookup"><span data-stu-id="8c3ae-138">Type</span></span>     | <span data-ttu-id="8c3ae-139">Kötelező</span><span class="sxs-lookup"><span data-stu-id="8c3ae-139">Required</span></span> | <span data-ttu-id="8c3ae-140">Leírás</span><span class="sxs-lookup"><span data-stu-id="8c3ae-140">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="8c3ae-141">Piac</span><span class="sxs-lookup"><span data-stu-id="8c3ae-141">Market</span></span>                      | <span data-ttu-id="8c3ae-142">sztring</span><span class="sxs-lookup"><span data-stu-id="8c3ae-142">string</span></span>   | <span data-ttu-id="8c3ae-143">Igen</span><span class="sxs-lookup"><span data-stu-id="8c3ae-143">Yes</span></span>       | <span data-ttu-id="8c3ae-144">Kétbetűs országkód a kért piachoz</span><span class="sxs-lookup"><span data-stu-id="8c3ae-144">Two letter country code for the market being requested</span></span>       |
|<span data-ttu-id="8c3ae-145">PricesheetView</span><span class="sxs-lookup"><span data-stu-id="8c3ae-145">PricesheetView</span></span> | <span data-ttu-id="8c3ae-146">sztring</span><span class="sxs-lookup"><span data-stu-id="8c3ae-146">string</span></span>   | <span data-ttu-id="8c3ae-147">Igen</span><span class="sxs-lookup"><span data-stu-id="8c3ae-147">Yes</span></span>       | <span data-ttu-id="8c3ae-148">A kért árlap típusa, amely nem azure_consumption, azure_reservations frissíthető.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-148">The type of price sheet being requested, this can be azure_consumption, azure_reservations or updatedlicensebased.</span></span>  |

> [!Note]
> <span data-ttu-id="8c3ae-149">A updatedlicensebased PriceSheetView jelenleg csak olyan partnerek számára érhető el, akik az M365/D365 új kereskedelmi felhasználói élmény technikai előzetes kiadásának részei.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-149">updatedlicensebased PriceSheetView is currently available only to partners who are part of the M365/D365 new commerce experience technical preview.</span></span>

### <a name="uri-filter-parameters"></a><span data-ttu-id="8c3ae-150">URI-szűrőparaméterek</span><span class="sxs-lookup"><span data-stu-id="8c3ae-150">URI filter parameters</span></span>

<span data-ttu-id="8c3ae-151">Használja az alábbi szűrőparamétereket.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-151">Use the following filter parameters.</span></span>

| <span data-ttu-id="8c3ae-152">Név</span><span class="sxs-lookup"><span data-stu-id="8c3ae-152">Name</span></span>                   | <span data-ttu-id="8c3ae-153">Típus</span><span class="sxs-lookup"><span data-stu-id="8c3ae-153">Type</span></span>     | <span data-ttu-id="8c3ae-154">Kötelező</span><span class="sxs-lookup"><span data-stu-id="8c3ae-154">Required</span></span> | <span data-ttu-id="8c3ae-155">Leírás</span><span class="sxs-lookup"><span data-stu-id="8c3ae-155">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="8c3ae-156">Idővonal</span><span class="sxs-lookup"><span data-stu-id="8c3ae-156">Timeline</span></span>| <span data-ttu-id="8c3ae-157">sztring</span><span class="sxs-lookup"><span data-stu-id="8c3ae-157">string</span></span>   | <span data-ttu-id="8c3ae-158">No</span><span class="sxs-lookup"><span data-stu-id="8c3ae-158">No</span></span>| <span data-ttu-id="8c3ae-159">Az alapértelmezett érték az aktuális, ha nem ad át értéket.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-159">Defaults to current if not passed.</span></span> <span data-ttu-id="8c3ae-160">Lehetséges értékek: előzmények, aktuális és jövőbeli.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-160">Possible values are history, current and future.</span></span>       |
|<span data-ttu-id="8c3ae-161">Month (hónap)</span><span class="sxs-lookup"><span data-stu-id="8c3ae-161">Month</span></span>| <span data-ttu-id="8c3ae-162">sztring</span><span class="sxs-lookup"><span data-stu-id="8c3ae-162">string</span></span>   | <span data-ttu-id="8c3ae-163">No</span><span class="sxs-lookup"><span data-stu-id="8c3ae-163">No</span></span>| <span data-ttu-id="8c3ae-164">Csak akkor szükséges, ha az előzmények lekérése meg van kérve, meg kell felelnie az YYYYMM értéknek a kért árlaphoz.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-164">Only required if history is requested, must adhere to YYYYMM for the price sheet being requested.</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="8c3ae-165">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="8c3ae-165">Request headers</span></span>

- <span data-ttu-id="8c3ae-166">További [információ: Partner REST-fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="8c3ae-166">See [Partner REST headers](headers.md) for more information.</span></span>

<span data-ttu-id="8c3ae-167">A fenti fejlécek mellett a díjszabási fájlok tömörített sávszélesség-csökkentő és letöltési időként is lekért fájlokként olvashatók be.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-167">In addition to the above headers, pricing files can be retrieved as compressed reducing bandwidth and download times.</span></span> <span data-ttu-id="8c3ae-168">Alapértelmezés szerint a fájlok nincsenek tömörítve.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-168">By default the files are not compressed.</span></span> <span data-ttu-id="8c3ae-169">A fájlok tömörített verzióit az alábbi fejlécértékkel kaphatja meg.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-169">To get compressed versions of the files you can include the below header value.</span></span> <span data-ttu-id="8c3ae-170">Ne feledni, hogy a tömörített lapok csak 2020 áprilisától érhetők el, a 2020 áprilisa előtti lapok csak nem tömörítettként érhetők el.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-170">Realize that compressed sheets are only available from April 2020 onward, all sheets prior to April 2020 are only available as not compressed.</span></span>

| <span data-ttu-id="8c3ae-171">Fejléc</span><span class="sxs-lookup"><span data-stu-id="8c3ae-171">Header</span></span>                   | <span data-ttu-id="8c3ae-172">Érték típusa</span><span class="sxs-lookup"><span data-stu-id="8c3ae-172">Value Type</span></span>     | <span data-ttu-id="8c3ae-173">Érték</span><span class="sxs-lookup"><span data-stu-id="8c3ae-173">Value</span></span> | <span data-ttu-id="8c3ae-174">Leírás</span><span class="sxs-lookup"><span data-stu-id="8c3ae-174">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="8c3ae-175">Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="8c3ae-175">Accept-Encoding</span></span>| <span data-ttu-id="8c3ae-176">sztring</span><span class="sxs-lookup"><span data-stu-id="8c3ae-176">string</span></span>   | <span data-ttu-id="8c3ae-177">Deflate</span><span class="sxs-lookup"><span data-stu-id="8c3ae-177">deflate</span></span>| <span data-ttu-id="8c3ae-178">Választható.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-178">Optional.</span></span> <span data-ttu-id="8c3ae-179">Ha nincs megadva, a fájlstream nem tömörített.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-179">If omitted file stream is not compressed.</span></span>       |

### <a name="request-example"></a><span data-ttu-id="8c3ae-180">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="8c3ae-180">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='ad',PricesheetView='azure_consumption')/$value?timeline=history&month=201909 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```
### <a name="request-example-for-new-commerce"></a><span data-ttu-id="8c3ae-181">Példa kérése új kereskedelemhez</span><span class="sxs-lookup"><span data-stu-id="8c3ae-181">Request example for new commerce</span></span>

> [!Note]
> <span data-ttu-id="8c3ae-182">A updatedlicensebased PriceSheetView jelenleg csak olyan partnerek számára érhető el, akik az M365/D365 új kereskedelmi felhasználói élmény technikai előzetes kiadásának részei.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-182">updatedlicensebased PriceSheetView is currently available only to partners who are part of the M365/D365 new commerce experience technical preview.</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='US',PricesheetView='updatedlicensebased')/$value?timeline=history&month=202101 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a><span data-ttu-id="8c3ae-183">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="8c3ae-183">REST response</span></span>

<span data-ttu-id="8c3ae-184">Ha a művelet sikeres, ez a metódus fájlstreamként adja vissza az árlistát.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-184">If successful, this method returns the price list as a file stream.</span></span> <span data-ttu-id="8c3ae-185">A fájlstream egy .csv fájl vagy a fájl tömörített .csv.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-185">File stream is either a .csv file or a zip compressed version of the .csv.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8c3ae-186">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="8c3ae-186">Response success and error codes</span></span>

<span data-ttu-id="8c3ae-187">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-187">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8c3ae-188">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-188">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8c3ae-189">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="8c3ae-189">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8c3ae-190">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="8c3ae-190">Response example</span></span>

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

### <a name="response-example-for-new-commerce"></a><span data-ttu-id="8c3ae-191">Válasz példa új kereskedelemre</span><span class="sxs-lookup"><span data-stu-id="8c3ae-191">Response example for new commerce</span></span>

> [!Note]
> <span data-ttu-id="8c3ae-192">A updatedlicensebased PriceSheetView jelenleg csak olyan partnerek számára érhető el, akik az M365/D365 új kereskedelmi felhasználói élmény technikai előzetes kiadásának részei.</span><span class="sxs-lookup"><span data-stu-id="8c3ae-192">updatedlicensebased PriceSheetView is currently available only to partners who are part of the M365/D365 new commerce experience technical preview.</span></span>

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
