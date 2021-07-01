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
# <a name="get-an-offer-matrix"></a><span data-ttu-id="23372-104">Ajánlatmátrix lekérte</span><span class="sxs-lookup"><span data-stu-id="23372-104">Get an offer matrix</span></span>

<span data-ttu-id="23372-105">A következőkre vonatkozik:</span><span class="sxs-lookup"><span data-stu-id="23372-105">Applies to:</span></span>

- <span data-ttu-id="23372-106">Partner API</span><span class="sxs-lookup"><span data-stu-id="23372-106">Partner API</span></span>
- <span data-ttu-id="23372-107">Az M365/D365 Új kereskedelmi élmény technikai előzetes verziója.</span><span class="sxs-lookup"><span data-stu-id="23372-107">The M365/D365 New Commerce experience technical preview.</span></span> <span data-ttu-id="23372-108">Az alábbi új kereskedelmi változások jelenleg csak az M365/D365 új kereskedelmi felhasználói élményének technikai előzetesében részt vesző partnerek számára érhetők el.</span><span class="sxs-lookup"><span data-stu-id="23372-108">The below New Commerce changes are currently available only to partners who are part of the M365/D365 new commerce experience technical preview.</span></span>

<span data-ttu-id="23372-109">Ez a témakör azt ismerteti, hogyan lehet lekért ajánlatmátrixot egy adott hónapra.</span><span class="sxs-lookup"><span data-stu-id="23372-109">This topic explains how to get an offer matrix for a given month.</span></span> <span data-ttu-id="23372-110">Az ajánlat mátrixa tulajdonságokat és vásárlási szabályokat tartalmaz a termékekhez és a terméktermékekhez.</span><span class="sxs-lookup"><span data-stu-id="23372-110">The offer matrix includes properties and purchase rules for the products and skus.</span></span> <span data-ttu-id="23372-111">Ez a metódus támogatja a szűrőket az előzmények havi lekért lekérthez.</span><span class="sxs-lookup"><span data-stu-id="23372-111">This method supports filters to get history by month.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="23372-112">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="23372-112">Prerequisites</span></span>

- <span data-ttu-id="23372-113">Az Partner API [ismertetett hitelesítő adatok.](api-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="23372-113">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="23372-114">Ez a forgatókönyv csak az alkalmazásfelhasználói hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="23372-114">This scenario only supports application user authentication.</span></span> <span data-ttu-id="23372-115">A csak alkalmazás még nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="23372-115">Application-only is not yet supported.</span></span> <span data-ttu-id="23372-116">A **HTTP-hibát:400 tapasztaló** partnereknek érdemes a Partner API [dokumentációját.](api-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="23372-116">Partners that experience **http error:400** should consult the [Partner API authentication](api-authentication.md) documentation.</span></span>
- <span data-ttu-id="23372-117">Ez az API jelenleg csak olyan felhasználói hozzáférést támogat, ahol a partnereknek a következő szerepkörök egyikében kell részt részte): globális rendszergazda, rendszergazdai ügynök vagy értékesítési ügynök.</span><span class="sxs-lookup"><span data-stu-id="23372-117">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Admin Agent or Sales Agent.</span></span>

## <a name="details"></a><span data-ttu-id="23372-118">Részletek</span><span class="sxs-lookup"><span data-stu-id="23372-118">Details</span></span>

- <span data-ttu-id="23372-119">A Current csak a frissített új kereskedelmi licencalapú termékek adatait adja vissza.</span><span class="sxs-lookup"><span data-stu-id="23372-119">Current returns data only for updated new commerce license-based products.</span></span>
- <span data-ttu-id="23372-120">Az aktuális díjszabás az API hívásának dátumig az aktuális hónapban elérhető termékeket tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="23372-120">Current pricing includes products available during the current month to the date the API is called.</span></span> <span data-ttu-id="23372-121">Az előző hónapok tartalmazzák a kiválasztott hónap utolsó napját.</span><span class="sxs-lookup"><span data-stu-id="23372-121">Previous months include date as of the last day of the selected month.</span></span>
- <span data-ttu-id="23372-122">Ez a metódus fájlstreamként ad vissza adatokat.</span><span class="sxs-lookup"><span data-stu-id="23372-122">This method returns data as a file stream.</span></span> <span data-ttu-id="23372-123">A fájlstream egy .csv fájl vagy a fájl tömörített .csv.</span><span class="sxs-lookup"><span data-stu-id="23372-123">File stream is either a .csv file or a zip compressed version of the .csv.</span></span> <span data-ttu-id="23372-124">A tömörített fájlok lekérésének részletei az alábbiakban olvashatók.</span><span class="sxs-lookup"><span data-stu-id="23372-124">Details about how to request compressed files are included below.</span></span>

## <a name="rest-request"></a><span data-ttu-id="23372-125">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="23372-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="23372-126">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="23372-126">Request syntax</span></span>

| <span data-ttu-id="23372-127">Metódus</span><span class="sxs-lookup"><span data-stu-id="23372-127">Method</span></span>   | <span data-ttu-id="23372-128">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="23372-128">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="23372-129">**Kap**</span><span class="sxs-lookup"><span data-stu-id="23372-129">**GET**</span></span> | <span data-ttu-id="23372-130"> https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month="{date}")/$value</span><span class="sxs-lookup"><span data-stu-id="23372-130">https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month='{date}')/$value</span></span> |

### <a name="uri-filter-parameters"></a><span data-ttu-id="23372-131">URI-szűrőparaméterek</span><span class="sxs-lookup"><span data-stu-id="23372-131">URI filter parameters</span></span>

<span data-ttu-id="23372-132">Használja az alábbi szűrőparamétereket.</span><span class="sxs-lookup"><span data-stu-id="23372-132">Use the following filter parameters.</span></span>

| <span data-ttu-id="23372-133">Név</span><span class="sxs-lookup"><span data-stu-id="23372-133">Name</span></span>                   | <span data-ttu-id="23372-134">Típus</span><span class="sxs-lookup"><span data-stu-id="23372-134">Type</span></span>     | <span data-ttu-id="23372-135">Kötelező</span><span class="sxs-lookup"><span data-stu-id="23372-135">Required</span></span> | <span data-ttu-id="23372-136">Leírás</span><span class="sxs-lookup"><span data-stu-id="23372-136">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="23372-137">Month (hónap)</span><span class="sxs-lookup"><span data-stu-id="23372-137">Month</span></span>| <span data-ttu-id="23372-138">sztring</span><span class="sxs-lookup"><span data-stu-id="23372-138">string</span></span>   | <span data-ttu-id="23372-139">No</span><span class="sxs-lookup"><span data-stu-id="23372-139">No</span></span> | <span data-ttu-id="23372-140">Meg kell felelnie az YYYYMM értéknek a kért árlaphoz.</span><span class="sxs-lookup"><span data-stu-id="23372-140">Must adhere to YYYYMM for the price sheet being requested.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="23372-141">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="23372-141">Request headers</span></span>

- <span data-ttu-id="23372-142">További [információ: Partner REST-fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="23372-142">See [Partner REST headers](headers.md) for more information.</span></span>

<span data-ttu-id="23372-143">A fenti fejlécek mellett a díjszabási fájlok tömörített sávszélesség-csökkentő és letöltési időként is lekért fájlokként olvashatók be.</span><span class="sxs-lookup"><span data-stu-id="23372-143">In addition to the above headers, pricing files can be retrieved as compressed reducing bandwidth and download times.</span></span> <span data-ttu-id="23372-144">Alapértelmezés szerint a fájlok nincsenek tömörítve.</span><span class="sxs-lookup"><span data-stu-id="23372-144">By default the files are not compressed.</span></span> <span data-ttu-id="23372-145">A fájlok tömörített verzióit az alábbi fejlécértékkel kaphatja meg.</span><span class="sxs-lookup"><span data-stu-id="23372-145">To get compressed versions of the files you can include the below header value.</span></span> <span data-ttu-id="23372-146">Ne feledni, hogy a tömörített lapok csak 2020 áprilisától érhetők el, a 2020 áprilisa előtti lapok csak nem tömörítettként érhetők el.</span><span class="sxs-lookup"><span data-stu-id="23372-146">Realize that compressed sheets are only available from April 2020 onward, all sheets prior to April 2020 are only available as not compressed.</span></span>

| <span data-ttu-id="23372-147">Fejléc</span><span class="sxs-lookup"><span data-stu-id="23372-147">Header</span></span>                   | <span data-ttu-id="23372-148">Érték típusa</span><span class="sxs-lookup"><span data-stu-id="23372-148">Value Type</span></span>     | <span data-ttu-id="23372-149">Érték</span><span class="sxs-lookup"><span data-stu-id="23372-149">Value</span></span> | <span data-ttu-id="23372-150">Leírás</span><span class="sxs-lookup"><span data-stu-id="23372-150">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="23372-151">Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="23372-151">Accept-Encoding</span></span>| <span data-ttu-id="23372-152">sztring</span><span class="sxs-lookup"><span data-stu-id="23372-152">string</span></span>   | <span data-ttu-id="23372-153">Deflate</span><span class="sxs-lookup"><span data-stu-id="23372-153">deflate</span></span>| <span data-ttu-id="23372-154">Választható.</span><span class="sxs-lookup"><span data-stu-id="23372-154">Optional.</span></span> <span data-ttu-id="23372-155">Ha nincs megadva, a fájlstream nem tömörített.</span><span class="sxs-lookup"><span data-stu-id="23372-155">If omitted file stream is not compressed.</span></span>       |

### <a name="request-example"></a><span data-ttu-id="23372-156">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="23372-156">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month='202101')/$value HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a><span data-ttu-id="23372-157">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="23372-157">REST response</span></span>

<span data-ttu-id="23372-158">Ha a művelet sikeres, ez a metódus egy ajánlatmátrixot ad vissza fájlstreamként.</span><span class="sxs-lookup"><span data-stu-id="23372-158">If successful, this method returns an offer matrix as a file stream.</span></span> <span data-ttu-id="23372-159">A fájlstream egy .csv fájl vagy a fájl tömörített .csv.</span><span class="sxs-lookup"><span data-stu-id="23372-159">File stream is either a .csv file or a zip compressed version of the .csv.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="23372-160">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="23372-160">Response success and error codes</span></span>

<span data-ttu-id="23372-161">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="23372-161">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="23372-162">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="23372-162">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="23372-163">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="23372-163">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="23372-164">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="23372-164">Response example</span></span>

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
