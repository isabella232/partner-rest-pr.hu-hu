---
title: Érdeklődő vagy lehetőség lekérése azonosító alapján
description: Érdeklődő vagy lehetőség beszerzése azonosító alapján.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: dcfaea393afc6a9d09946b4c31b7168ba26aa255
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770531"
---
# <a name="get-a-lead-or-opportunity-by-id"></a><span data-ttu-id="b3f55-103">Érdeklődő vagy lehetőség lekérése azonosító alapján</span><span class="sxs-lookup"><span data-stu-id="b3f55-103">Get a lead or opportunity by Id</span></span>

<span data-ttu-id="b3f55-104">A következőkre vonatkozik:</span><span class="sxs-lookup"><span data-stu-id="b3f55-104">Applies to:</span></span>

- <span data-ttu-id="b3f55-105">Partner API</span><span class="sxs-lookup"><span data-stu-id="b3f55-105">Partner API</span></span>

<span data-ttu-id="b3f55-106">Ez a témakör azt ismerteti, hogyan lehet az azonosító alapján érdeklődői vagy közös értékesítési lehetőséget szerezni.</span><span class="sxs-lookup"><span data-stu-id="b3f55-106">This topic explains how to get a lead or co-sell opportunity by Id.</span></span>

> [!Note]
> <span data-ttu-id="b3f55-107">A Microsoft kereskedelmi piactérről (Azure Marketplace és AppSource) kapott érdeklődők nem támogatottak.</span><span class="sxs-lookup"><span data-stu-id="b3f55-107">Leads received from the Microsoft commercial marketplace (Azure Marketplace and AppSource) are not supported.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b3f55-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="b3f55-108">Prerequisites</span></span>

- <span data-ttu-id="b3f55-109">A [partner API-hitelesítésben](api-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="b3f55-109">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="b3f55-110">Ez a forgatókönyv támogatja a hitelesítést az App + User hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="b3f55-110">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="b3f55-111">Ez az API jelenleg csak a felhasználói hozzáférést támogatja, ahol a partnereknek a következő szerepkörök egyikében kell lenniük: globális rendszergazda, hivatkozó rendszergazda vagy hivatkozó felhasználó.</span><span class="sxs-lookup"><span data-stu-id="b3f55-111">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Referral Admin or Referral User.</span></span>

## <a name="rest-request"></a><span data-ttu-id="b3f55-112">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="b3f55-112">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b3f55-113">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="b3f55-113">Request syntax</span></span>

| <span data-ttu-id="b3f55-114">Metódus</span><span class="sxs-lookup"><span data-stu-id="b3f55-114">Method</span></span>   | <span data-ttu-id="b3f55-115">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="b3f55-115">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b3f55-116">**GET**</span><span class="sxs-lookup"><span data-stu-id="b3f55-116">**GET**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}>                                     |

### <a name="uri-parameter"></a><span data-ttu-id="b3f55-117">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="b3f55-117">URI parameter</span></span>


| <span data-ttu-id="b3f55-118">Név</span><span class="sxs-lookup"><span data-stu-id="b3f55-118">Name</span></span>                   | <span data-ttu-id="b3f55-119">Típus</span><span class="sxs-lookup"><span data-stu-id="b3f55-119">Type</span></span>     | <span data-ttu-id="b3f55-120">Kötelező</span><span class="sxs-lookup"><span data-stu-id="b3f55-120">Required</span></span> | <span data-ttu-id="b3f55-121">Leírás</span><span class="sxs-lookup"><span data-stu-id="b3f55-121">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="b3f55-122">Id</span><span class="sxs-lookup"><span data-stu-id="b3f55-122">Id</span></span>                      | <span data-ttu-id="b3f55-123">sztring</span><span class="sxs-lookup"><span data-stu-id="b3f55-123">string</span></span>   | <span data-ttu-id="b3f55-124">Igen</span><span class="sxs-lookup"><span data-stu-id="b3f55-124">Yes</span></span>       | <span data-ttu-id="b3f55-125">Az érdeklődő vagy a közös értékesítés lehetőség egyedi azonosítója</span><span class="sxs-lookup"><span data-stu-id="b3f55-125">The unique identifier for a lead or co-sell opportunity</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="b3f55-126">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="b3f55-126">Request headers</span></span>

<span data-ttu-id="b3f55-127">További információért lásd: [partner Rest-fejlécek](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="b3f55-127">See [Partner REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="b3f55-128">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="b3f55-128">Request body</span></span>

<span data-ttu-id="b3f55-129">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="b3f55-129">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b3f55-130">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="b3f55-130">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id} HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
```

## <a name="rest-response"></a><span data-ttu-id="b3f55-131">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="b3f55-131">REST response</span></span>

<span data-ttu-id="b3f55-132">Ha a művelet sikeres, a válasz törzse tartalmazza az azonosítóhoz tartozó [érdeklődőt vagy lehetőséget](referral-resources.md) .</span><span class="sxs-lookup"><span data-stu-id="b3f55-132">If successful, the response body contains the [lead or opportunity](referral-resources.md) matching the Id.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b3f55-133">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="b3f55-133">Response success and error codes</span></span>

<span data-ttu-id="b3f55-134">Minden válaszhoz tartozik egy [http-állapotkód](error-codes.md) , amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="b3f55-134">Each response comes with an [HTTP status code](error-codes.md) that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b3f55-135">A kód, a hiba típusa és a további paraméterek beolvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="b3f55-135">Use a network trace tool to read this code, the error type, and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="b3f55-136">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="b3f55-136">Response example</span></span>

``` http
HTTP/1.1 200 OK
Content-Type: application/json
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731

{
    "@odata.context": "https://api.partner.microsoft.com/v1.0/engagments/referrals/$metadata#Referrals/$entity",
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
      "notes": "We are interested in deploying Microsoft 365 and are looking forsupport in training our employees. Can you help?",
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
        "uri": "https://api.partner.microsoft.com/v1.0/engagements/referrals$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'",
        "method": "GET"
      },
      "self": {
        "uri": "https://api.partner.microsoft.com/v1.0/engagements/referralsc5fbb3b6-be74-4795-9fb5-4324c73fed37",
        "method": "GET"
      }
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\""
}
```

> [!Note]
> <span data-ttu-id="b3f55-137">A fenti példában illustratration lévő mezők nem teljesek.</span><span class="sxs-lookup"><span data-stu-id="b3f55-137">The fields in the example illustratration above are not exhaustive.</span></span> <span data-ttu-id="b3f55-138">A tényleges API-válasz több mezőt is tartalmaz, például az ügyfél és a partner csapatát.</span><span class="sxs-lookup"><span data-stu-id="b3f55-138">The actual API response contains more fields like the customer and partner teams.</span></span> <span data-ttu-id="b3f55-139">A támogatott mezők teljes listáját az [Ajánlói erőforrások](referral-resources.md)című részben tekintheti meg.</span><span class="sxs-lookup"><span data-stu-id="b3f55-139">For the full list of supported fields, see [referral resources](referral-resources.md).</span></span>