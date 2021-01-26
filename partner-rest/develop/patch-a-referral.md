---
title: Érdeklődő vagy lehetőség frissítése
description: Lehetővé teszi az érdeklődő vagy a lehetőség részleteinek frissítését.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: abfe7308f46cd65b9358b369f6fa05bcca4c1df2
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770542"
---
# <a name="update-a-lead-or-opportunity"></a><span data-ttu-id="173a7-103">Érdeklődő vagy lehetőség frissítése</span><span class="sxs-lookup"><span data-stu-id="173a7-103">Update a lead or opportunity</span></span>

<span data-ttu-id="173a7-104">A következőkre vonatkozik:</span><span class="sxs-lookup"><span data-stu-id="173a7-104">Applies to:</span></span>

- <span data-ttu-id="173a7-105">Partner API</span><span class="sxs-lookup"><span data-stu-id="173a7-105">Partner API</span></span>

<span data-ttu-id="173a7-106">Ez a témakör azt ismerteti, hogyan frissítheti az érdeklődők vagy a lehetőségek részleteit, például az ügylet értékét, a becsült zárási dátumot, illetve az értékesítési fázisok kezelését a további részletek között.</span><span class="sxs-lookup"><span data-stu-id="173a7-106">This topic explains how to update the lead or opportunity details like the deal value, estimated close date or manage the sales stages amongst other details.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="173a7-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="173a7-107">Prerequisites</span></span>

- <span data-ttu-id="173a7-108">A [partner API-hitelesítésben](api-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="173a7-108">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="173a7-109">Ez a forgatókönyv támogatja a hitelesítést az App + User hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="173a7-109">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="173a7-110">Ez az API jelenleg csak a felhasználói hozzáférést támogatja, ahol a partnereknek a következő szerepkörök egyikében kell lenniük: globális rendszergazda, hivatkozó rendszergazda vagy hivatkozó felhasználó.</span><span class="sxs-lookup"><span data-stu-id="173a7-110">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Referral Admin or Referral User.</span></span>

## <a name="rest-request"></a><span data-ttu-id="173a7-111">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="173a7-111">REST Request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="173a7-112">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="173a7-112">Request syntax</span></span>

| <span data-ttu-id="173a7-113">Metódus</span><span class="sxs-lookup"><span data-stu-id="173a7-113">Method</span></span>  | <span data-ttu-id="173a7-114">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="173a7-114">Request URI</span></span>                                                       |
|---------|-------------------------------------------------------------------|
| <span data-ttu-id="173a7-115">**JAVÍTÁS**</span><span class="sxs-lookup"><span data-stu-id="173a7-115">**PATCH**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}> |

### <a name="uri-parameter"></a><span data-ttu-id="173a7-116">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="173a7-116">URI parameter</span></span>


| <span data-ttu-id="173a7-117">Név</span><span class="sxs-lookup"><span data-stu-id="173a7-117">Name</span></span>                   | <span data-ttu-id="173a7-118">Típus</span><span class="sxs-lookup"><span data-stu-id="173a7-118">Type</span></span>     | <span data-ttu-id="173a7-119">Kötelező</span><span class="sxs-lookup"><span data-stu-id="173a7-119">Required</span></span> | <span data-ttu-id="173a7-120">Leírás</span><span class="sxs-lookup"><span data-stu-id="173a7-120">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="173a7-121">Id</span><span class="sxs-lookup"><span data-stu-id="173a7-121">Id</span></span>                      | <span data-ttu-id="173a7-122">sztring</span><span class="sxs-lookup"><span data-stu-id="173a7-122">string</span></span>   | <span data-ttu-id="173a7-123">Igen</span><span class="sxs-lookup"><span data-stu-id="173a7-123">Yes</span></span>       | <span data-ttu-id="173a7-124">Az érdeklődő vagy a közös értékesítés lehetőség egyedi azonosítója</span><span class="sxs-lookup"><span data-stu-id="173a7-124">The unique identifier for a lead or co-sell opportunity</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="173a7-125">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="173a7-125">Request headers</span></span>

<span data-ttu-id="173a7-126">További információért lásd: [partner Rest-fejlécek](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="173a7-126">See [Partner REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="173a7-127">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="173a7-127">Request body</span></span>

<span data-ttu-id="173a7-128">A kérelem törzse a [JSON-javító](https://tools.ietf.org/html/rfc6902) formátumot követi.</span><span class="sxs-lookup"><span data-stu-id="173a7-128">The request body follows the [Json Patch](https://tools.ietf.org/html/rfc6902) format.</span></span> <span data-ttu-id="173a7-129">A JSON-javítási dokumentumok tömbje műveletekből áll.</span><span class="sxs-lookup"><span data-stu-id="173a7-129">A JSON Patch document has an array of operations.</span></span> <span data-ttu-id="173a7-130">Minden művelet egy adott típusú változást azonosít.</span><span class="sxs-lookup"><span data-stu-id="173a7-130">Each operation identifies a particular type of change.</span></span> <span data-ttu-id="173a7-131">Ilyen változások például egy tömb elem hozzáadása vagy egy tulajdonságérték cseréje.</span><span class="sxs-lookup"><span data-stu-id="173a7-131">Examples of such changes include adding an array element or replacing a property value.</span></span>

> [!Important]
> <span data-ttu-id="173a7-132">Az API jelenleg csak a `replace` és a `add` műveleteket támogatja.</span><span class="sxs-lookup"><span data-stu-id="173a7-132">The API currently only supports the `replace` and `add` operations.</span></span>

### <a name="request-example"></a><span data-ttu-id="173a7-133">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="173a7-133">Request example</span></span>

```http
PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
Authorization: Bearer <token>
Content-Type: application/json
Prefer: return=representation

[
    {
        "op": "replace",
        "path": "/details/dealValue",
        "value": "10000"
    },
    {
        "op": "add",
        "path": "/team/-",
        "value": {
            "email": "jane.doe@contoso.com",
            "firstName": "Jane",
            "lastName": "Doe",
            "phoneNumber": "0000000001"
        }
    }
]
```

> [!Note]
> <span data-ttu-id="173a7-134">Ha a rendszer átadja az **IF-Match** fejlécet, a rendszer a Egyidejűség vezérlésére használja.</span><span class="sxs-lookup"><span data-stu-id="173a7-134">If the **If-Match** header is passed, it will be used for concurrency control.</span></span>

## <a name="rest-response"></a><span data-ttu-id="173a7-135">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="173a7-135">REST Response</span></span>

<span data-ttu-id="173a7-136">Ha a művelet sikeres, a válasz törzse tartalmazza a frissített [érdeklődőt vagy lehetőséget](referral-resources.md).</span><span class="sxs-lookup"><span data-stu-id="173a7-136">If successful, the response body contains the updated [lead or opportunity](referral-resources.md).</span></span>


### <a name="response-success-and-error-codes"></a><span data-ttu-id="173a7-137">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="173a7-137">Response success and error codes</span></span>

<span data-ttu-id="173a7-138">Minden válaszhoz tartozik egy [http-állapotkód](error-codes.md) , amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="173a7-138">Each response comes with an [HTTP status code](error-codes.md) that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="173a7-139">A kód, a hiba típusa és a további paraméterek beolvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="173a7-139">Use a network trace tool to read this code, the error type, and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="173a7-140">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="173a7-140">Response example</span></span>

``` http
HTTP/1.1 204 No Content
Content-Length: 0
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
```

> [!Tip]
> <span data-ttu-id="173a7-141">A válasz törzse a **preferált** fejléctől függ.</span><span class="sxs-lookup"><span data-stu-id="173a7-141">The response body depends on the **Prefer** header.</span></span> <span data-ttu-id="173a7-142">Ha a fejléc értéke nincs megadva a kérelemben, a válasz törzse üres, és a 204-es HTTP-állapotkód szerepel.</span><span class="sxs-lookup"><span data-stu-id="173a7-142">If the header value is omitted in the request, the response body is empty with a HTTP Status code 204.</span></span> <span data-ttu-id="173a7-143">Adja hozzá a `Prefer: return=representation` fejlécet a frissített érdeklődő vagy lehetőség beszerzéséhez.</span><span class="sxs-lookup"><span data-stu-id="173a7-143">Add `Prefer: return=representation` to the header to get the updated lead or opportunity.</span></span>

## <a name="sample-requests"></a><span data-ttu-id="173a7-144">Példák a kérelmekre</span><span class="sxs-lookup"><span data-stu-id="173a7-144">Sample requests</span></span>

1. <span data-ttu-id="173a7-145">Frissíti az ügylet értékét a lehetőség 10000-re, és frissíti a megjegyzéseket.</span><span class="sxs-lookup"><span data-stu-id="173a7-145">Updates the deal value for the opportunity to 10000 and updates the notes.</span></span> <span data-ttu-id="173a7-146">A fejléc absense miatt nincs egyidejűségi ellenőrzés `If-Match` .</span><span class="sxs-lookup"><span data-stu-id="173a7-146">There are no concurrency checks because of the absense of the `If-Match` header.</span></span>
    
    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    
    [
        {"op":"replace","path":"/details/dealValue","value":"10000"},
        {"op":"replace","path":"/details/notes","value":"Lorem ipsum dolor sit amet."}
    ]
    ```

2. <span data-ttu-id="173a7-147">Egy érdeklődő vagy egy megnyert lehetőség állapotát frissíti.</span><span class="sxs-lookup"><span data-stu-id="173a7-147">Updates the status of a lead or opportunity to Won.</span></span>
    
    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    
    [
        {"op":"replace", "path":"/status", "value":"Closed"},
        {"op":"replace", "path":"/substatus", "value":"Won"}
    ]
    ```

    > [!Important]
    > <span data-ttu-id="173a7-148">A `status` és a `substatus` mezőnek meg kell felelnie az [itt](referral-resources.md)leírtak szerinti átmeneti értékek megengedett készletének.</span><span class="sxs-lookup"><span data-stu-id="173a7-148">The `status` and `substatus` fields should conform to the allowed set of transition values as described [here](referral-resources.md).</span></span>

3. <span data-ttu-id="173a7-149">Új tagot ad hozzá a szervezethez az érdeklődő vagy a lehetőség csapatához.</span><span class="sxs-lookup"><span data-stu-id="173a7-149">Adds a new member from your organization to the lead or opportunity team.</span></span> <span data-ttu-id="173a7-150">A válasz a fejléc jelenléte miatt a frissített érdeklődőt vagy lehetőséget fogja tartalmazni `Prefer: return=representation` .</span><span class="sxs-lookup"><span data-stu-id="173a7-150">The response will contain the updated lead or opportunity because of the presence of the `Prefer: return=representation` header.</span></span>

    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    Prefer: return=representation
    
    [
        {
            "op": "add",
            "path": "/team/-",
            "value": {
                "email": "jane.doe@contoso.com",
                "firstName": "Jane",
                "lastName": "Doe",
                "phoneNumber": "0000000001"
            }
        }
    ]
    ```
