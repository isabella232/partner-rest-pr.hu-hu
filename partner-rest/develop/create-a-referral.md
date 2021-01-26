---
title: Javaslat létrehozása
description: Hozzon létre független vagy megosztott hivatkozásokat a partner API-ban.
ms.date: 05/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 6aab4b5f45030c3c16294b2929b1a6d3086fb951
ms.sourcegitcommit: 3c165938f544ff226cbe11ca21ed5aa00448d9b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2020
ms.locfileid: "97770494"
---
# <a name="create-a-referral"></a><span data-ttu-id="5db64-103">Javaslat létrehozása</span><span class="sxs-lookup"><span data-stu-id="5db64-103">Create a referral</span></span>

<span data-ttu-id="5db64-104">A következőkre vonatkozik:</span><span class="sxs-lookup"><span data-stu-id="5db64-104">Applies to:</span></span>

- <span data-ttu-id="5db64-105">Partner API</span><span class="sxs-lookup"><span data-stu-id="5db64-105">Partner API</span></span>

<span data-ttu-id="5db64-106">Ez a témakör az átirányítások létrehozását ismerteti.</span><span class="sxs-lookup"><span data-stu-id="5db64-106">This topic explains how to create a referral.</span></span> <span data-ttu-id="5db64-107">Kétféle [ReferralType](referral-resources.md#referraltype)létezik:</span><span class="sxs-lookup"><span data-stu-id="5db64-107">There are two types of [ReferralType](referral-resources.md#referraltype):</span></span>

1. <span data-ttu-id="5db64-108">Független: Ha egy hivatkozás egy partner számára látható.</span><span class="sxs-lookup"><span data-stu-id="5db64-108">Independent: Where a referral is visible to one partner.</span></span>
2. <span data-ttu-id="5db64-109">Shared: Ha egy hivatkozás két, egymással együttműködő fél számára látható.</span><span class="sxs-lookup"><span data-stu-id="5db64-109">Shared: Where a referral is visible to two parties that are working together.</span></span> <span data-ttu-id="5db64-110">Ha például a Microsoft és egy partner együttes értékesítési ügylettel dolgozik együtt, akkor mindkét fél megoszthatja az átirányítást.</span><span class="sxs-lookup"><span data-stu-id="5db64-110">For example, if Microsoft and a partner are working together in a co-selling deal, a referral can be shared between both parties.</span></span> <span data-ttu-id="5db64-111">További információ: [megosztott hivatkozás létrehozása](#create-a-shared-referral).</span><span class="sxs-lookup"><span data-stu-id="5db64-111">For more information, see the section [Creating a shared referral](#create-a-shared-referral).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5db64-112">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="5db64-112">Prerequisites</span></span>

- <span data-ttu-id="5db64-113">A [partner API-hitelesítésben](api-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="5db64-113">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="5db64-114">Ez a forgatókönyv támogatja a hitelesítést az App + User hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="5db64-114">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="5db64-115">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="5db64-115">REST Request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5db64-116">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="5db64-116">Request syntax</span></span>

| <span data-ttu-id="5db64-117">Metódus</span><span class="sxs-lookup"><span data-stu-id="5db64-117">Method</span></span>  | <span data-ttu-id="5db64-118">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="5db64-118">Request URI</span></span>                                                  |
|---------|--------------------------------------------------------------|
| <span data-ttu-id="5db64-119">**UTÁNI**</span><span class="sxs-lookup"><span data-stu-id="5db64-119">**POST**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals> |

### <a name="request-headers"></a><span data-ttu-id="5db64-120">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="5db64-120">Request headers</span></span>

- <span data-ttu-id="5db64-121">További információért lásd: [partner API Rest-fejlécek](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="5db64-121">See [Partner API REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="5db64-122">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="5db64-122">Request body</span></span>

<span data-ttu-id="5db64-123">Ez a tábla a kérelem törzsének [hivatkozó](referral-resources.md) tulajdonságait írja le egy új hivatkozáshoz.</span><span class="sxs-lookup"><span data-stu-id="5db64-123">This table describes the [Referral](referral-resources.md) properties in the request body for a brand new referral.</span></span>

| <span data-ttu-id="5db64-124">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="5db64-124">Property</span></span>            | <span data-ttu-id="5db64-125">Típus</span><span class="sxs-lookup"><span data-stu-id="5db64-125">Type</span></span>                                                                 | <span data-ttu-id="5db64-126">Leírás</span><span class="sxs-lookup"><span data-stu-id="5db64-126">Description</span></span>                                                                                                          |
|---------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5db64-127">Név</span><span class="sxs-lookup"><span data-stu-id="5db64-127">Name</span></span>                | <span data-ttu-id="5db64-128">sztring</span><span class="sxs-lookup"><span data-stu-id="5db64-128">string</span></span>                                                               | <span data-ttu-id="5db64-129">Az ajánló neve.</span><span class="sxs-lookup"><span data-stu-id="5db64-129">The name of the Referral.</span></span>                                                                                            |
| <span data-ttu-id="5db64-130">ExternalReferenceId</span><span class="sxs-lookup"><span data-stu-id="5db64-130">ExternalReferenceId</span></span> | <span data-ttu-id="5db64-131">sztring</span><span class="sxs-lookup"><span data-stu-id="5db64-131">string</span></span>                                                               | <span data-ttu-id="5db64-132">Az átirányításhoz tartozó külső azonosító.</span><span class="sxs-lookup"><span data-stu-id="5db64-132">An external identifier for the referral.</span></span> <span data-ttu-id="5db64-133">Például a saját Dynamics 365 ólom vagy a lehetőség azonosítója.</span><span class="sxs-lookup"><span data-stu-id="5db64-133">For example, your own Dynamics 365 lead or opportunity ID.</span></span>                   |
| <span data-ttu-id="5db64-134">Állapot</span><span class="sxs-lookup"><span data-stu-id="5db64-134">Status</span></span>              | [<span data-ttu-id="5db64-135">ReferralStatus</span><span class="sxs-lookup"><span data-stu-id="5db64-135">ReferralStatus</span></span>](referral-resources.md#referralstatus)               | <span data-ttu-id="5db64-136">Egy [enumerálás](https://docs.microsoft.com/dotnet/api/system.enum) az átirányítási állapotot jelző értékekkel.</span><span class="sxs-lookup"><span data-stu-id="5db64-136">An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral status.</span></span>          |
| <span data-ttu-id="5db64-137">Részállapot</span><span class="sxs-lookup"><span data-stu-id="5db64-137">Substatus</span></span>           | [<span data-ttu-id="5db64-138">ReferralSubstatus</span><span class="sxs-lookup"><span data-stu-id="5db64-138">ReferralSubstatus</span></span>](referral-resources.md#referralsubstatus)         | <span data-ttu-id="5db64-139">Az átirányítási alállapotot jelző értékekkel rendelkező [enumerálás](https://docs.microsoft.com/dotnet/api/system.enum) .</span><span class="sxs-lookup"><span data-stu-id="5db64-139">An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral substatus.</span></span>       |
| <span data-ttu-id="5db64-140">StatusReason</span><span class="sxs-lookup"><span data-stu-id="5db64-140">StatusReason</span></span>        | <span data-ttu-id="5db64-141">sztring</span><span class="sxs-lookup"><span data-stu-id="5db64-141">string</span></span>                                                               | <span data-ttu-id="5db64-142">Az állapottal kapcsolatos leíró üzenet.</span><span class="sxs-lookup"><span data-stu-id="5db64-142">A descriptive message about the status.</span></span> <span data-ttu-id="5db64-143">Például magyarázza el, miért vesztette el az átirányítást.</span><span class="sxs-lookup"><span data-stu-id="5db64-143">For example, explain why the referral was lost.</span></span>                            |
| <span data-ttu-id="5db64-144">ReferralType</span><span class="sxs-lookup"><span data-stu-id="5db64-144">ReferralType</span></span>        | [<span data-ttu-id="5db64-145">ReferralType</span><span class="sxs-lookup"><span data-stu-id="5db64-145">ReferralType</span></span>](referral-resources.md#referraltype)                   | <span data-ttu-id="5db64-146">Az átirányítási típust jelöli.</span><span class="sxs-lookup"><span data-stu-id="5db64-146">Represents the referral type.</span></span> <span data-ttu-id="5db64-147">**Szükséges.**</span><span class="sxs-lookup"><span data-stu-id="5db64-147">**Required.**</span></span>                                                                                        |
| <span data-ttu-id="5db64-148">Minősítés</span><span class="sxs-lookup"><span data-stu-id="5db64-148">Qualification</span></span>       | [<span data-ttu-id="5db64-149">ReferralQualification</span><span class="sxs-lookup"><span data-stu-id="5db64-149">ReferralQualification</span></span>](referral-resources.md#referralqualification) | <span data-ttu-id="5db64-150">Az ajánló minőségét jelöli.</span><span class="sxs-lookup"><span data-stu-id="5db64-150">Represents the quality of the referral.</span></span>                                                                              |
| <span data-ttu-id="5db64-151">CustomerProfile</span><span class="sxs-lookup"><span data-stu-id="5db64-151">CustomerProfile</span></span>     | [<span data-ttu-id="5db64-152">CustomerProfile</span><span class="sxs-lookup"><span data-stu-id="5db64-152">CustomerProfile</span></span>](referral-resources.md#customerprofile)             | <span data-ttu-id="5db64-153">Ügyfél kapcsolattartási adatai.</span><span class="sxs-lookup"><span data-stu-id="5db64-153">Customer contact information.</span></span>  <span data-ttu-id="5db64-154">**Szükséges.**</span><span class="sxs-lookup"><span data-stu-id="5db64-154">**Required.**</span></span>                                                                                      |
| <span data-ttu-id="5db64-155">Hozzájárulás</span><span class="sxs-lookup"><span data-stu-id="5db64-155">Consent</span></span>             | [<span data-ttu-id="5db64-156">Hozzájárulás</span><span class="sxs-lookup"><span data-stu-id="5db64-156">Consent</span></span>](referral-resources.md#consent)                             | <span data-ttu-id="5db64-157">A hozzájárulási jelzők az információk megosztását más szervezetekkel, és lehetővé teszik a felhasználóknak való kapcsolatfelvételt. **Kötelező megadni.**</span><span class="sxs-lookup"><span data-stu-id="5db64-157">Consent flags around sharing information with other organizations and allowing them to contact users.**Required.**</span></span>               |
| <span data-ttu-id="5db64-158">Részletek</span><span class="sxs-lookup"><span data-stu-id="5db64-158">Details</span></span>             | [<span data-ttu-id="5db64-159">ReferralDetails</span><span class="sxs-lookup"><span data-stu-id="5db64-159">ReferralDetails</span></span>](referral-resources.md#referraldetails)             | <span data-ttu-id="5db64-160">Vásárlói adatok, megjegyzések, ügyleti érték, pénznem zárási dátuma.</span><span class="sxs-lookup"><span data-stu-id="5db64-160">Customer details, notes, deal value, currency closing date.</span></span> <span data-ttu-id="5db64-161">**Szükséges.**</span><span class="sxs-lookup"><span data-stu-id="5db64-161">**Required.**</span></span>                                                           |
| <span data-ttu-id="5db64-162">Csoport</span><span class="sxs-lookup"><span data-stu-id="5db64-162">Team</span></span>                | [<span data-ttu-id="5db64-163">Tag</span><span class="sxs-lookup"><span data-stu-id="5db64-163">Member</span></span>](referral-resources.md#member)                               | <span data-ttu-id="5db64-164">A partneri szerepvállalásban részt vevő szervezetekben lévő felhasználókat jelöli.</span><span class="sxs-lookup"><span data-stu-id="5db64-164">Represents users in the organizations that are involved in the partner engagement.</span></span>                                   |
| <span data-ttu-id="5db64-165">InviteContext</span><span class="sxs-lookup"><span data-stu-id="5db64-165">InviteContext</span></span>       | [<span data-ttu-id="5db64-166">InviteContext</span><span class="sxs-lookup"><span data-stu-id="5db64-166">InviteContext</span></span>](referral-resources.md#invitecontext)                 | <span data-ttu-id="5db64-167">A felhasználó által megadható további információkat jelenít meg egy másik szervezetnek a partneri szerepvállaláshoz való meghívásakor.</span><span class="sxs-lookup"><span data-stu-id="5db64-167">Represents additional information a user can provide when inviting another organization into the partner engagement.</span></span> |
| <span data-ttu-id="5db64-168">Cél</span><span class="sxs-lookup"><span data-stu-id="5db64-168">Target</span></span>         | [<span data-ttu-id="5db64-169">ReferralTarget</span><span class="sxs-lookup"><span data-stu-id="5db64-169">ReferralTarget</span></span>](referral-resources.md#target)        | <span data-ttu-id="5db64-170">A felhasználó által megadható további információkat jelenít meg egy másik szervezetnek a partneri szerepvállaláshoz való meghívásakor.</span><span class="sxs-lookup"><span data-stu-id="5db64-170">Represents additional information a user can provide when inviting another organization into the partner engagement.</span></span>  |

#### <a name="status--substatus-transition-states"></a><span data-ttu-id="5db64-171">Állapot & állapot átmeneti állapotai</span><span class="sxs-lookup"><span data-stu-id="5db64-171">Status & Substatus transition states</span></span>

| <span data-ttu-id="5db64-172">Állapot</span><span class="sxs-lookup"><span data-stu-id="5db64-172">Status</span></span> | <span data-ttu-id="5db64-173">Engedélyezett állapot-váltás</span><span class="sxs-lookup"><span data-stu-id="5db64-173">Allowed status transition</span></span> | <span data-ttu-id="5db64-174">Engedélyezett alállapot</span><span class="sxs-lookup"><span data-stu-id="5db64-174">Allowed substatus</span></span>            |
|--------|---------------------------|------------------------------|
| <span data-ttu-id="5db64-175">Új</span><span class="sxs-lookup"><span data-stu-id="5db64-175">New</span></span>    | <span data-ttu-id="5db64-176">Új, aktív, lezárt</span><span class="sxs-lookup"><span data-stu-id="5db64-176">New, Active, Closed</span></span>       | <span data-ttu-id="5db64-177">Függőben, fogadva</span><span class="sxs-lookup"><span data-stu-id="5db64-177">Pending, Received</span></span>            |
| <span data-ttu-id="5db64-178">Aktív</span><span class="sxs-lookup"><span data-stu-id="5db64-178">Active</span></span> | <span data-ttu-id="5db64-179">Aktív, lezárt</span><span class="sxs-lookup"><span data-stu-id="5db64-179">Active, Closed</span></span>            | <span data-ttu-id="5db64-180">Elfogadva</span><span class="sxs-lookup"><span data-stu-id="5db64-180">Accepted</span></span>                     |
| <span data-ttu-id="5db64-181">Lezárt</span><span class="sxs-lookup"><span data-stu-id="5db64-181">Closed</span></span> | <span data-ttu-id="5db64-182">Lezárt</span><span class="sxs-lookup"><span data-stu-id="5db64-182">Closed</span></span>                    | <span data-ttu-id="5db64-183">Megnyert, elveszett, visszautasított, lejárt</span><span class="sxs-lookup"><span data-stu-id="5db64-183">Won, Lost, Declined, Expired</span></span> |

### <a name="request-example"></a><span data-ttu-id="5db64-184">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="5db64-184">Request example</span></span>

```http
POST https://api.partner.microsoft.com/v1.0/engagements/referrals HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

 {
    "name": "Test Cosell Invite_20",
    "status": "New",
    "substatus": "Pending",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Shared",
    "target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-34104-EBB"
        }
    ],
    "customerProfile": {
        "name": "Contoso Customer Inc",
        "address": {
            "addressLine1": "One Microsoft Way",
            "addressLine2": "34",
            "city": "Redmond",
            "state": "WA",
            "postalCode": "98052",
            "country": "US"
        },
        "size": "10to50employees",
        "team": [
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Sue",
                "lastName": "Smith",
                "phoneNumber": "1234567890",
                "email": "sue.smith@contoso.com"
            },
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Joe",
                "lastName": "Hansen",
                "phoneNumber": "4035698759",
                "email": "joe.hansen@contoso.com"
            }
        ],
        "ids": []
    },
    "consent": {
        "consentToToShareInfoWithOthers": true,
        "consentToContact": true
    },
    "details": {
        "notes": "Customer is looking to leverage Dynamics 365 to manage their supply chain. There is also a need to leverage a set of custom apps to enable their business processes.",
        "dealValue": 50000,
        "currency": "USD",
        "closingDateTime": "2018-11-14T00:00:00Z",
        "requirements": {
            "industries": [
                {
                    "id": "Manufacturing"
                }
            ],
            "products": [
                {
                    "id": "Dynamics365Enterprise"
                }
            ],
            "services": [
                {
                    "id": "DeploymentOrMigration"
                }
            ],
            "solutions": [
                {
                    "name": "Dynamics 365 for Field Service",
                    "type": "Category",
                    "id": "Dynamics365forFieldService"
                }
            ]
        }
    },
    "team": [
        {
            "contactPreference": {
                "locale": "en-us",
                "disableNotifications": false
            },
            "firstName": "John",
            "lastName": "Doe",
            "phoneNumber": "1231231234",
            "email": "john.doe@microsoft.com"
        }
    ],
    "inviteContext": {
        "notes": "Hi ABC Partner, hoping you can help this customer. Thanks, John @ Microsoft",
        "invitedBy": {
            "organizationId": "msft"
        }
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="5db64-185">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="5db64-185">REST Response</span></span>

<span data-ttu-id="5db64-186">Ha ez sikeres, ez a metódus a válasz törzsében lévő felszámított [hivatkozó](referral-resources.md) erőforrást adja vissza.</span><span class="sxs-lookup"><span data-stu-id="5db64-186">If successful, this method returns the populated [Referral](referral-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5db64-187">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="5db64-187">Response success and error codes</span></span>

<span data-ttu-id="5db64-188">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="5db64-188">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5db64-189">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="5db64-189">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5db64-190">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5db64-190">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5db64-191">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="5db64-191">Response example</span></span>

``` http
{
    "id": "4111fffc-f9ee-4d53-bba6-569135228642",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Contoso Company",
    "name": "Test Cosell Invite_20",
    "externalReferenceId": null,
    "createdDateTime": "2019-02-23T02:05:23.2931817Z",
    "updatedDateTime": "2019-02-23T02:05:23.2931817Z",
    "expirationDateTime": null,
    "status": "Active",
    "substatus": "Accepted",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Shared",
    "eTag": "\"00006d10-0000-0000-0000-5c70aa630000\"",
    "target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-34104-EBB"
        }
    ],
    "customerProfile": {
        "name": "Contoso Customer Inc",
        "address": {
            "addressLine1": "One Microsoft Way",
            "addressLine2": "34",
            "city": "Redmond",
            "state": "WA",
            "postalCode": "98052",
            "country": "US"
        },
        "size": "10to50employees",
        "team": [
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Sue",
                "lastName": "Smith",
                "phoneNumber": "1234567890",
                "email": "sue.smith@contoso.com"
            },
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Joe",
                "lastName": "Hansen",
                "phoneNumber": "4035698759",
                "email": "joe.hansen@contoso.com"
            }
        ],
        "ids": []
    },
    "consent": {
        "consentToToShareInfoWithOthers": true,
        "consentToContact": true
    },
    "details": {
        "notes": "Customer is looking to leverage Dynamics 365 to manage their supply chain. There is also a need to leverage a set of custom apps to enable their business processes.",
        "dealValue": 50000,
        "currency": "USD",
        "requirements": {
            "industries": [
                {
                    "id": "Manufacturing"
                }
            ],
            "products": [
                {
                    "id": "Dynamics365Enterprise"
                }
            ],
            "services": [
                {
                    "id": "DeploymentOrMigration"
                }
            ],
            "solutions": [
                {
                    "name": "Dynamics 365 for Field Service",
                    "type": "Category",
                    "id": "Dynamics365forFieldService"
                }
            ]
        }
    },
    "team": [
        {
            "contactPreference": {
                "locale": "en-us",
                "disableNotifications": false
            },
            "firstName": "John",
            "lastName": "Doe",
            "phoneNumber": "1231231234",
            "email": "john.doe@microsoft.com"
        }
    ],
    "inviteContext": {
        "notes": "Hi ABC Partner, hoping you can help this customer. Thanks, John @ Microsoft",
        "invitedBy": {
            "organizationId": "msft"
        }
    },
    "links": {
        "relatedReferrals": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals?$filter=engagementId eq '37ef26aa-1d15-4533-9f93-a69bd33ab1e5'",
            "method": "GET"
        },
        "self": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals/4111fffc-f9ee-4d53-bba6-569135228642",
            "method": "GET"
        }
    }
}
```

## <a name="create-a-shared-referral"></a><span data-ttu-id="5db64-192">Megosztott hivatkozás létrehozása</span><span class="sxs-lookup"><span data-stu-id="5db64-192">Create a shared referral</span></span>

<span data-ttu-id="5db64-193">A **megosztott** [átirányítási típushoz](referral-resources.md#referraltype)tartozó hivatkozás létrehozásának két lépése van.</span><span class="sxs-lookup"><span data-stu-id="5db64-193">There are two steps to create a referral of the **Shared** [referral type](referral-resources.md#referraltype).</span></span>

1. [<span data-ttu-id="5db64-194">Megosztott hivatkozás létrehozása</span><span class="sxs-lookup"><span data-stu-id="5db64-194">Create your shared referral</span></span>](#create-your-referral)
2. [<span data-ttu-id="5db64-195">Csatlakoztatott hivatkozás létrehozása a második fél számára</span><span class="sxs-lookup"><span data-stu-id="5db64-195">Create a connected referral for the second party</span></span>](#create-a-connected-referral)

<span data-ttu-id="5db64-196">A következő folyamatábra ezt a két lépést mutatja be egy megosztott hivatkozó létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="5db64-196">The following flow chart illustrates these two steps in creating a shared referral.</span></span>

![A Microsoft partner API-n keresztül összekapcsolt két hivatkozással megosztott átirányítást bemutató folyamatábra](../images/SharedReferral.png)

### <a name="create-your-referral"></a><span data-ttu-id="5db64-198">Az ajánló létrehozása</span><span class="sxs-lookup"><span data-stu-id="5db64-198">Create your referral</span></span>

1. <span data-ttu-id="5db64-199">Hozzon létre egy [ReferralType](referral-resources.md#referraltype) -készlettel megosztott hivatkozást.</span><span class="sxs-lookup"><span data-stu-id="5db64-199">Create a referral with [ReferralType](referral-resources.md#referraltype) set to shared.</span></span>
2. <span data-ttu-id="5db64-200">Másolja a **engagementId** a visszatérési válaszból.</span><span class="sxs-lookup"><span data-stu-id="5db64-200">Copy the **engagementId** from the return response.</span></span>

<span data-ttu-id="5db64-201">[ReferralTarget](referral-resources.md#target) minta az átirányításhoz</span><span class="sxs-lookup"><span data-stu-id="5db64-201">[ReferralTarget](referral-resources.md#target) sample for referral</span></span>

```json
"target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-ABC-DEF"
        }
    ]
```

### <a name="create-a-connected-referral"></a><span data-ttu-id="5db64-202">Csatlakoztatott hivatkozás létrehozása</span><span class="sxs-lookup"><span data-stu-id="5db64-202">Create a connected referral</span></span>

1. <span data-ttu-id="5db64-203">Hozzon létre egy másik hivatkozást a Microsoft számára.</span><span class="sxs-lookup"><span data-stu-id="5db64-203">Create another referral for Microsoft.</span></span>
2. <span data-ttu-id="5db64-204">Adja meg a **enagementId** az átirányításból, hogy azok össze legyenek kötve.</span><span class="sxs-lookup"><span data-stu-id="5db64-204">Include the **enagementId** from your referral so they are tied together.</span></span>

<span data-ttu-id="5db64-205">[ReferralTarget](referral-resources.md#target) minta a Microsoft Referral szolgáltatáshoz</span><span class="sxs-lookup"><span data-stu-id="5db64-205">[ReferralTarget](referral-resources.md#target) sample for Microsoft referral</span></span>

```json
"target": [
        {
            "type": "BusinessProfileLocation",
            "id": "msft"
        }
    ]
```