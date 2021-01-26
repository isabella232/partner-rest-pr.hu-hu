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
# <a name="get-the-list-of-leads-and-opportunities"></a><span data-ttu-id="b8b7f-103">Érdeklődők és lehetőségek listájának lekérése</span><span class="sxs-lookup"><span data-stu-id="b8b7f-103">Get the list of leads and opportunities</span></span>

<span data-ttu-id="b8b7f-104">A következőkre vonatkozik:</span><span class="sxs-lookup"><span data-stu-id="b8b7f-104">Applies to:</span></span>

- <span data-ttu-id="b8b7f-105">Partner API</span><span class="sxs-lookup"><span data-stu-id="b8b7f-105">Partner API</span></span>

 <span data-ttu-id="b8b7f-106">Ez a témakör bemutatja, hogyan kérheti le a Microsoft-megoldások szolgáltatójának oldaláról érkező érdeklődők listáját, és a Microsoft-értékesítők vagy más partnerek által fogadott közös értékesítési lehetőségeket.</span><span class="sxs-lookup"><span data-stu-id="b8b7f-106">This topic explains how to get the list of leads received from Microsoft solution provider page and co-sell opportunities received from Microsoft sellers or other partners.</span></span> <span data-ttu-id="b8b7f-107">Ez a művelet a szervezet által létrehozott közös értékesítési lehetőségek vagy folyamat-ajánlatok listáját is beolvassa.</span><span class="sxs-lookup"><span data-stu-id="b8b7f-107">This will also fetch the list of co-sell opportunities or pipeline deals created by your organization.</span></span>

> [!Note]
> <span data-ttu-id="b8b7f-108">A Microsoft kereskedelmi piactérről (Azure Marketplace és AppSource) kapott érdeklődők nem támogatottak.</span><span class="sxs-lookup"><span data-stu-id="b8b7f-108">Leads received from the Microsoft commercial marketplace (Azure Marketplace and AppSource) are not supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8b7f-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="b8b7f-109">Prerequisites</span></span>

- <span data-ttu-id="b8b7f-110">A [partner API-hitelesítésben](api-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="b8b7f-110">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="b8b7f-111">Ez a forgatókönyv támogatja a hitelesítést az App + User hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="b8b7f-111">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="b8b7f-112">Ez az API jelenleg csak a felhasználói hozzáférést támogatja, ahol a partnereknek a következő szerepkörök egyikében kell lenniük: globális rendszergazda, hivatkozó rendszergazda vagy hivatkozó felhasználó.</span><span class="sxs-lookup"><span data-stu-id="b8b7f-112">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Referral Admin or Referral User.</span></span>

## <a name="rest-request"></a><span data-ttu-id="b8b7f-113">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="b8b7f-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b8b7f-114">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="b8b7f-114">Request syntax</span></span>

| <span data-ttu-id="b8b7f-115">Metódus</span><span class="sxs-lookup"><span data-stu-id="b8b7f-115">Method</span></span>  | <span data-ttu-id="b8b7f-116">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="b8b7f-116">Request URI</span></span>                                                    |
|:--------|:---------------------------------------------------------------|
| <span data-ttu-id="b8b7f-117">**GET**</span><span class="sxs-lookup"><span data-stu-id="b8b7f-117">**GET**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals> |

#### <a name="supported-odata-operations"></a><span data-ttu-id="b8b7f-118">Támogatott OData-műveletek</span><span class="sxs-lookup"><span data-stu-id="b8b7f-118">Supported OData operations</span></span>

| <span data-ttu-id="b8b7f-119">Név</span><span class="sxs-lookup"><span data-stu-id="b8b7f-119">Name</span></span>     | <span data-ttu-id="b8b7f-120">Leírás</span><span class="sxs-lookup"><span data-stu-id="b8b7f-120">Description</span></span>     | <span data-ttu-id="b8b7f-121">Kötelező</span><span class="sxs-lookup"><span data-stu-id="b8b7f-121">Required</span></span>    | <span data-ttu-id="b8b7f-122">Példa</span><span class="sxs-lookup"><span data-stu-id="b8b7f-122">Example</span></span>                                                                                                                                                                                                                                                     |
|:---------|:----------------|:------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b8b7f-123">$select</span><span class="sxs-lookup"><span data-stu-id="b8b7f-123">$select</span></span>  | <span data-ttu-id="b8b7f-124">Mezők kiválasztása</span><span class="sxs-lookup"><span data-stu-id="b8b7f-124">Selects fields</span></span>  | <span data-ttu-id="b8b7f-125">Nem</span><span class="sxs-lookup"><span data-stu-id="b8b7f-125">No</span></span>          | `/referrals?$select=id,status,customerProfile`                                                                                                                                                                                                              |
| <span data-ttu-id="b8b7f-126">$filter</span><span class="sxs-lookup"><span data-stu-id="b8b7f-126">$filter</span></span>  | <span data-ttu-id="b8b7f-127">Szűrők eredményei</span><span class="sxs-lookup"><span data-stu-id="b8b7f-127">Filters results</span></span> | <span data-ttu-id="b8b7f-128">Ajánlott</span><span class="sxs-lookup"><span data-stu-id="b8b7f-128">Recommended</span></span> | `/referrals?$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'` <br/> `/referrals?$filter=status eq 'New' and qualification eq 'SalesQualified'` <br/> `/referrals?$filter=customerProfile/address/country eq 'US' and direction eq 'Incoming'` |
| <span data-ttu-id="b8b7f-129">$orderby</span><span class="sxs-lookup"><span data-stu-id="b8b7f-129">$orderby</span></span> | <span data-ttu-id="b8b7f-130">Megrendelések eredményei</span><span class="sxs-lookup"><span data-stu-id="b8b7f-130">Orders results</span></span>  | <span data-ttu-id="b8b7f-131">Ajánlott</span><span class="sxs-lookup"><span data-stu-id="b8b7f-131">Recommended</span></span> | `/referrals?$orderby=createdDateTime desc`                                                                                                                                                                                                                  |

#### <a name="supported-orderby-parameters"></a><span data-ttu-id="b8b7f-132">Támogatott OrderBy paraméterek</span><span class="sxs-lookup"><span data-stu-id="b8b7f-132">Supported orderby parameters</span></span>

<span data-ttu-id="b8b7f-133">A következő $orderby paraméterekkel rendezheti az érdeklődők és a lehetőségek listáját</span><span class="sxs-lookup"><span data-stu-id="b8b7f-133">Use the following $orderby parameters to sort the list of leads and opportunities</span></span>

| <span data-ttu-id="b8b7f-134">Név</span><span class="sxs-lookup"><span data-stu-id="b8b7f-134">Name</span></span>            | <span data-ttu-id="b8b7f-135">Típus</span><span class="sxs-lookup"><span data-stu-id="b8b7f-135">Type</span></span>     | <span data-ttu-id="b8b7f-136">Leírás</span><span class="sxs-lookup"><span data-stu-id="b8b7f-136">Description</span></span>                                       |
|:----------------|:---------|:--------------------------------------------------|
| <span data-ttu-id="b8b7f-137">createdDateTime</span><span class="sxs-lookup"><span data-stu-id="b8b7f-137">createdDateTime</span></span> | <span data-ttu-id="b8b7f-138">DateTime</span><span class="sxs-lookup"><span data-stu-id="b8b7f-138">DateTime</span></span> | <span data-ttu-id="b8b7f-139">Az érdeklődő vagy a lehetőség létrehozásának dátuma és időpontja</span><span class="sxs-lookup"><span data-stu-id="b8b7f-139">Creation date and time of the lead or opportunity</span></span> |
| <span data-ttu-id="b8b7f-140">updatedDateTime</span><span class="sxs-lookup"><span data-stu-id="b8b7f-140">updatedDateTime</span></span> | <span data-ttu-id="b8b7f-141">DateTime</span><span class="sxs-lookup"><span data-stu-id="b8b7f-141">DateTime</span></span> | <span data-ttu-id="b8b7f-142">Az érdeklődő vagy a lehetőség dátumának és idejének frissítése</span><span class="sxs-lookup"><span data-stu-id="b8b7f-142">Update date and time of the lead or opportunity</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="b8b7f-143">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="b8b7f-143">Request headers</span></span>

<span data-ttu-id="b8b7f-144">További információért lásd: [partner Rest-fejlécek](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="b8b7f-144">See [Partner REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="b8b7f-145">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="b8b7f-145">Request body</span></span>

<span data-ttu-id="b8b7f-146">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="b8b7f-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b8b7f-147">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="b8b7f-147">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$orderby=createdDateTime desc HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
```

## <a name="rest-response"></a><span data-ttu-id="b8b7f-148">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="b8b7f-148">REST response</span></span>

<span data-ttu-id="b8b7f-149">Ha ez sikeres, a válasz törzse [érdeklődőket és/vagy lehetőségeket](referral-resources.md)tartalmazó gyűjteményt tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="b8b7f-149">If successful, the response body contains a collection of [leads and/or opportunities](referral-resources.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b8b7f-150">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="b8b7f-150">Response success and error codes</span></span>

<span data-ttu-id="b8b7f-151">Minden válaszhoz tartozik egy [http-állapotkód](error-codes.md) , amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="b8b7f-151">Each response comes with an [HTTP status code](error-codes.md) that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b8b7f-152">A kód, a hiba típusa és a további paraméterek beolvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="b8b7f-152">Use a network trace tool to read this code, the error type, and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="b8b7f-153">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="b8b7f-153">Response example</span></span>

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

<span data-ttu-id="b8b7f-154">Az `@odata.nextLink` eredmények következő oldalának beszerzéséhez használja a t.</span><span class="sxs-lookup"><span data-stu-id="b8b7f-154">Use the `@odata.nextLink` to get the next page of results.</span></span>

> [!Note]
> <span data-ttu-id="b8b7f-155">A fenti példában illustratration lévő mezők nem teljesek.</span><span class="sxs-lookup"><span data-stu-id="b8b7f-155">The fields in the example illustratration above are not exhaustive.</span></span> <span data-ttu-id="b8b7f-156">A tényleges API-válasz több mezőt is tartalmaz, például az ügyfél és a partner csapatát.</span><span class="sxs-lookup"><span data-stu-id="b8b7f-156">The actual API response contains more fields like the customer and partner teams.</span></span> <span data-ttu-id="b8b7f-157">A támogatott mezők teljes listáját az [Ajánlói erőforrások](referral-resources.md)című részben tekintheti meg.</span><span class="sxs-lookup"><span data-stu-id="b8b7f-157">For the full list of supported fields, see [referral resources](referral-resources.md).</span></span>

## <a name="sample-requests"></a><span data-ttu-id="b8b7f-158">Példák a kérelmekre</span><span class="sxs-lookup"><span data-stu-id="b8b7f-158">Sample requests</span></span>

1. <span data-ttu-id="b8b7f-159">Az első 10 legutóbbi bejövő közös értékesítési lehetőség beolvasása.</span><span class="sxs-lookup"><span data-stu-id="b8b7f-159">Gets the top 10 most recent inbound co-sell opportunities.</span></span> <span data-ttu-id="b8b7f-160">A kérelem beolvassa a Microsoft értékesítési képviselő vagy egy másik partner által kezdeményezett lehetőségeket, meghívja a szervezetet, hogy részt vegyen a közös értékesítési tevékenységben.</span><span class="sxs-lookup"><span data-stu-id="b8b7f-160">The request will fetch opportunities initiated by a Microsoft sales representative or another partner, inviting your organization to participate in a co-selling activity.</span></span>
    
    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$top=10&$filter=(type eq 'Shared' and direction eq 'Incoming')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```

2. <span data-ttu-id="b8b7f-161">Beolvassa a legutóbbi bejövő érdeklődőket és lehetőségeket, amelyeket nem válaszolt.</span><span class="sxs-lookup"><span data-stu-id="b8b7f-161">Gets the most recent inbound leads and opportunities that have not been responded to.</span></span>  

    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$top=10&$filter=(direction eq 'Incoming' and substatus eq 'Pending')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```

    > [!Important]
    > <span data-ttu-id="b8b7f-162">Ha nem válaszol egy érdeklődőre vagy lehetőségre a megadott időn belül (jelenleg 14 nap), archiváljuk a lejárt módon, és értesítjük a Microsoftot vagy a partnert, aki ezt a lehetőséget elküldte.</span><span class="sxs-lookup"><span data-stu-id="b8b7f-162">If you don't respond to a lead or opportunity within the allotted time (currently 14 days), we'll archive it as Expired and notify either Microsoft or the partner who sent you this opportunity.</span></span>

3. <span data-ttu-id="b8b7f-163">Beolvassa a szervezete által kezdeményezett legutóbbi aktív közös értékesítési lehetőségeket, amelyeket egy adott értékesítő dolgoz fel.</span><span class="sxs-lookup"><span data-stu-id="b8b7f-163">Gets the most recent active co-sell opportunities initiated by your organization and being worked on by a specific seller.</span></span>
    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$filter=status eq 'Active' and direction eq 'Outgoing' and type eq 'Shared' and team/any(t:t/email eq 'r2d2@contoso.com')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```