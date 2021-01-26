---
title: Érdeklődő vagy lehetőség frissítése (elavult)
description: Lehetővé teszi az érdeklődő vagy a lehetőség részleteinek frissítését. Ez a módszer egy érdeklődő vagy lehetőség frissítésére elavult, és ehelyett a recommmend használja.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 9705db1c21dbec7099cfefebdc7bb23ec65e428c
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770543"
---
# <a name="update-a-lead-or-opportunity-obsolete"></a><span data-ttu-id="801f7-104">Érdeklődő vagy lehetőség frissítése (elavult)</span><span class="sxs-lookup"><span data-stu-id="801f7-104">Update a lead or opportunity (Obsolete)</span></span>

<span data-ttu-id="801f7-105">A következőkre vonatkozik:</span><span class="sxs-lookup"><span data-stu-id="801f7-105">Applies to:</span></span>

- <span data-ttu-id="801f7-106">Partner API</span><span class="sxs-lookup"><span data-stu-id="801f7-106">Partner API</span></span>

<span data-ttu-id="801f7-107">Ez a témakör azt ismerteti, hogyan frissítheti az érdeklődők vagy a lehetőségek részleteit, például az ügylet értékét, a becsült zárási dátumot, illetve az értékesítési fázisok kezelését a további részletek között.</span><span class="sxs-lookup"><span data-stu-id="801f7-107">This topic explains how to update the lead or opportunity details like the deal value, estimated close date or manage the sales stages amongst other details.</span></span> 


> [!IMPORTANT]
<span data-ttu-id="801f7-108">Ez a módszer egy érdeklődő vagy lehetőség frissítésére elavult, és [Ehelyett a recommmend](patch-a-referral.md) használja.</span><span class="sxs-lookup"><span data-stu-id="801f7-108">This method of updating a lead or opportunity is obsolete and we recommmend using the [PATCH](patch-a-referral.md) call instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="801f7-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="801f7-109">Prerequisites</span></span>

- <span data-ttu-id="801f7-110">A [partner API-hitelesítésben](api-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="801f7-110">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="801f7-111">Ez a forgatókönyv támogatja a hitelesítést az App + User hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="801f7-111">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="801f7-112">Ez az API jelenleg csak a felhasználói hozzáférést támogatja, ahol a partnereknek a következő szerepkörök egyikében kell lenniük: globális rendszergazda, hivatkozó rendszergazda vagy hivatkozó felhasználó.</span><span class="sxs-lookup"><span data-stu-id="801f7-112">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Referral Admin or Referral User.</span></span>

## <a name="rest-request"></a><span data-ttu-id="801f7-113">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="801f7-113">REST Request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="801f7-114">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="801f7-114">Request syntax</span></span>

| <span data-ttu-id="801f7-115">Metódus</span><span class="sxs-lookup"><span data-stu-id="801f7-115">Method</span></span>  | <span data-ttu-id="801f7-116">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="801f7-116">Request URI</span></span>                                                       |
|---------|-------------------------------------------------------------------|
| <span data-ttu-id="801f7-117">**PUT**</span><span class="sxs-lookup"><span data-stu-id="801f7-117">**PUT**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}> |

### <a name="request-headers"></a><span data-ttu-id="801f7-118">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="801f7-118">Request headers</span></span>

- <span data-ttu-id="801f7-119">További információ: [partner API Rest-fejlécek](headers.md).</span><span class="sxs-lookup"><span data-stu-id="801f7-119">For more information, see [Partner API REST headers](headers.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="801f7-120">Ügyeljen arra, hogy az **IF-Match** fejlécet adja meg.</span><span class="sxs-lookup"><span data-stu-id="801f7-120">Be sure to set the **If-Match** header.</span></span>

### <a name="request-body"></a><span data-ttu-id="801f7-121">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="801f7-121">Request body</span></span>

<span data-ttu-id="801f7-122">Ez a táblázat a kérés törzsének [hivatkozó](referral-resources.md) tulajdonságait ismerteti.</span><span class="sxs-lookup"><span data-stu-id="801f7-122">This table describes the [Referral](referral-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="801f7-123">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="801f7-123">Property</span></span>            | <span data-ttu-id="801f7-124">Típus</span><span class="sxs-lookup"><span data-stu-id="801f7-124">Type</span></span>                                                                 | <span data-ttu-id="801f7-125">Leírás</span><span class="sxs-lookup"><span data-stu-id="801f7-125">Description</span></span>                                                                                                          |
|---------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="801f7-126">Id</span><span class="sxs-lookup"><span data-stu-id="801f7-126">Id</span></span>                  | <span data-ttu-id="801f7-127">sztring</span><span class="sxs-lookup"><span data-stu-id="801f7-127">string</span></span>                                                               | <span data-ttu-id="801f7-128">Az átirányításhoz tartozó azonosító.</span><span class="sxs-lookup"><span data-stu-id="801f7-128">The ID for this Referral.</span></span>                                                                                            |
| <span data-ttu-id="801f7-129">EngagementId</span><span class="sxs-lookup"><span data-stu-id="801f7-129">EngagementId</span></span>        | <span data-ttu-id="801f7-130">sztring</span><span class="sxs-lookup"><span data-stu-id="801f7-130">string</span></span>                                                               | <span data-ttu-id="801f7-131">Az ajánló EngagementID.</span><span class="sxs-lookup"><span data-stu-id="801f7-131">The EngagementID for this Referral.</span></span> <span data-ttu-id="801f7-132">Több hivatkozás is társítható egyetlen EngagementID</span><span class="sxs-lookup"><span data-stu-id="801f7-132">Multiple referrals can be associated to a single EngagementID</span></span>                    |
| <span data-ttu-id="801f7-133">Name</span><span class="sxs-lookup"><span data-stu-id="801f7-133">Name</span></span>                | <span data-ttu-id="801f7-134">sztring</span><span class="sxs-lookup"><span data-stu-id="801f7-134">string</span></span>                                                               | <span data-ttu-id="801f7-135">Az ajánló neve.</span><span class="sxs-lookup"><span data-stu-id="801f7-135">The name of the Referral.</span></span>                                                                                            |
| <span data-ttu-id="801f7-136">ExternalReferenceId</span><span class="sxs-lookup"><span data-stu-id="801f7-136">ExternalReferenceId</span></span> | <span data-ttu-id="801f7-137">sztring</span><span class="sxs-lookup"><span data-stu-id="801f7-137">string</span></span>                                                               | <span data-ttu-id="801f7-138">Az átirányításhoz tartozó külső azonosító.</span><span class="sxs-lookup"><span data-stu-id="801f7-138">An external identifier for the referral.</span></span> <span data-ttu-id="801f7-139">Példa: saját Dynamics 365 érdeklődő/lehetőség AZONOSÍTÓjának tárolása</span><span class="sxs-lookup"><span data-stu-id="801f7-139">Example: Store your own Dynamics 365 lead/opportunity ID</span></span>                    |
| <span data-ttu-id="801f7-140">CreatedDateTime</span><span class="sxs-lookup"><span data-stu-id="801f7-140">CreatedDateTime</span></span>     | <span data-ttu-id="801f7-141">karakterlánc UTC-dátum időformátuma</span><span class="sxs-lookup"><span data-stu-id="801f7-141">string in UTC date time format</span></span>                                       | <span data-ttu-id="801f7-142">Az átirányítás létrehozásának dátuma.</span><span class="sxs-lookup"><span data-stu-id="801f7-142">The date the referral was created.</span></span>                                                                                   |
| <span data-ttu-id="801f7-143">UpdatedDateTime</span><span class="sxs-lookup"><span data-stu-id="801f7-143">UpdatedDateTime</span></span>     | <span data-ttu-id="801f7-144">karakterlánc UTC-dátum időformátuma</span><span class="sxs-lookup"><span data-stu-id="801f7-144">string in UTC date time format</span></span>                                       | <span data-ttu-id="801f7-145">Az átirányítás utolsó frissítésének dátuma.</span><span class="sxs-lookup"><span data-stu-id="801f7-145">The date the referral was last updated.</span></span>                                                                              |
| <span data-ttu-id="801f7-146">ExpirationDateTime</span><span class="sxs-lookup"><span data-stu-id="801f7-146">ExpirationDateTime</span></span>  | <span data-ttu-id="801f7-147">karakterlánc UTC-dátum időformátuma</span><span class="sxs-lookup"><span data-stu-id="801f7-147">string in UTC date time format</span></span>                                       | <span data-ttu-id="801f7-148">Az átirányítás érvényességének dátuma.</span><span class="sxs-lookup"><span data-stu-id="801f7-148">The date the referral will expire.</span></span>                                                                                   |
| <span data-ttu-id="801f7-149">Állapot</span><span class="sxs-lookup"><span data-stu-id="801f7-149">Status</span></span>              | [<span data-ttu-id="801f7-150">ReferralStatus</span><span class="sxs-lookup"><span data-stu-id="801f7-150">ReferralStatus</span></span>](referral-resources.md#referralstatus)               | <span data-ttu-id="801f7-151">Egy [enumerálás](https://docs.microsoft.com/dotnet/api/system.enum) az átirányítási állapotot jelző értékekkel.</span><span class="sxs-lookup"><span data-stu-id="801f7-151">An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral status.</span></span>          |
| <span data-ttu-id="801f7-152">Részállapot</span><span class="sxs-lookup"><span data-stu-id="801f7-152">Substatus</span></span>           | [<span data-ttu-id="801f7-153">ReferralSubstatus</span><span class="sxs-lookup"><span data-stu-id="801f7-153">ReferralSubstatus</span></span>](referral-resources.md#referralsubstatus)         | <span data-ttu-id="801f7-154">Az átirányítási alállapotot jelző értékekkel rendelkező [enumerálás](https://docs.microsoft.com/dotnet/api/system.enum) .</span><span class="sxs-lookup"><span data-stu-id="801f7-154">An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral sub status.</span></span>      |
| <span data-ttu-id="801f7-155">StatusReason</span><span class="sxs-lookup"><span data-stu-id="801f7-155">StatusReason</span></span>        | <span data-ttu-id="801f7-156">sztring</span><span class="sxs-lookup"><span data-stu-id="801f7-156">string</span></span>                                                               | <span data-ttu-id="801f7-157">Az állapottal kapcsolatos leíró üzenet.</span><span class="sxs-lookup"><span data-stu-id="801f7-157">A descriptive message about the status.</span></span> <span data-ttu-id="801f7-158">Például magyarázza el, miért vesztette el az átirányítást.</span><span class="sxs-lookup"><span data-stu-id="801f7-158">For example, explain why the referral was lost.</span></span>                              |
| <span data-ttu-id="801f7-159">ReferralType</span><span class="sxs-lookup"><span data-stu-id="801f7-159">ReferralType</span></span>        | [<span data-ttu-id="801f7-160">ReferralType</span><span class="sxs-lookup"><span data-stu-id="801f7-160">ReferralType</span></span>](referral-resources.md#referraltype)                   | <span data-ttu-id="801f7-161">Az átirányítási típust jelöli.</span><span class="sxs-lookup"><span data-stu-id="801f7-161">Represents the referral type.</span></span>                                                                                        |
| <span data-ttu-id="801f7-162">Minősítés</span><span class="sxs-lookup"><span data-stu-id="801f7-162">Qualification</span></span>       | [<span data-ttu-id="801f7-163">ReferralQualification</span><span class="sxs-lookup"><span data-stu-id="801f7-163">ReferralQualification</span></span>](referral-resources.md#referralqualification) | <span data-ttu-id="801f7-164">Az ajánló minőségét jelöli.</span><span class="sxs-lookup"><span data-stu-id="801f7-164">Represents the quality of the referral.</span></span>                                                                              |
| <span data-ttu-id="801f7-165">CustomerProfile</span><span class="sxs-lookup"><span data-stu-id="801f7-165">CustomerProfile</span></span>     | [<span data-ttu-id="801f7-166">CustomerProfile</span><span class="sxs-lookup"><span data-stu-id="801f7-166">CustomerProfile</span></span>](referral-resources.md#customerprofile)             | <span data-ttu-id="801f7-167">Ügyfél kapcsolattartási adatai.</span><span class="sxs-lookup"><span data-stu-id="801f7-167">Customer contact information.</span></span>                                                                                        |
| <span data-ttu-id="801f7-168">Hozzájárulás</span><span class="sxs-lookup"><span data-stu-id="801f7-168">Consent</span></span>             | [<span data-ttu-id="801f7-169">Hozzájárulás</span><span class="sxs-lookup"><span data-stu-id="801f7-169">Consent</span></span>](referral-resources.md#consent)                             | <span data-ttu-id="801f7-170">A hozzájárulási jelzők az információk megosztását más szervezetekkel, és lehetővé teszik a felhasználóknak való kapcsolatfelvételt.</span><span class="sxs-lookup"><span data-stu-id="801f7-170">Consent flags around sharing information with other organizations and allowing them to contact users.</span></span>                |
| <span data-ttu-id="801f7-171">Részletek</span><span class="sxs-lookup"><span data-stu-id="801f7-171">Details</span></span>             | [<span data-ttu-id="801f7-172">ReferralDetails</span><span class="sxs-lookup"><span data-stu-id="801f7-172">ReferralDetails</span></span>](referral-resources.md#referraldetails)             | <span data-ttu-id="801f7-173">Vásárlói adatok, megjegyzések, ügyleti érték, pénznem zárási dátuma.</span><span class="sxs-lookup"><span data-stu-id="801f7-173">Customer details, notes, deal value, currency closing date.</span></span>                                                          |
| <span data-ttu-id="801f7-174">Csoport</span><span class="sxs-lookup"><span data-stu-id="801f7-174">Team</span></span>                | [<span data-ttu-id="801f7-175">Tag</span><span class="sxs-lookup"><span data-stu-id="801f7-175">Member</span></span>](referral-resources.md#member)                               | <span data-ttu-id="801f7-176">A partneri szerepvállalásban részt vevő szervezetekben lévő felhasználókat jelöli.</span><span class="sxs-lookup"><span data-stu-id="801f7-176">Represents users in the organizations that are involved in the partner engagement.</span></span>                                   |
| <span data-ttu-id="801f7-177">InviteContext</span><span class="sxs-lookup"><span data-stu-id="801f7-177">InviteContext</span></span>       | [<span data-ttu-id="801f7-178">InviteContext</span><span class="sxs-lookup"><span data-stu-id="801f7-178">InviteContext</span></span>](referral-resources.md#invitecontext)                 | <span data-ttu-id="801f7-179">A felhasználó által megadható további információkat jelenít meg egy másik szervezetnek a partneri szerepvállaláshoz való meghívásakor.</span><span class="sxs-lookup"><span data-stu-id="801f7-179">Represents additional information a user can provide when inviting another organization into the partner engagement.</span></span> |
| <span data-ttu-id="801f7-180">Cél</span><span class="sxs-lookup"><span data-stu-id="801f7-180">Target</span></span>         | [<span data-ttu-id="801f7-181">ReferralTarget</span><span class="sxs-lookup"><span data-stu-id="801f7-181">ReferralTarget</span></span>](referral-resources.md#target)        | <span data-ttu-id="801f7-182">A felhasználó által megadható további információkat jelenít meg egy másik szervezetnek a partneri szerepvállaláshoz való meghívásakor.</span><span class="sxs-lookup"><span data-stu-id="801f7-182">Represents additional information a user can provide when inviting another organization into the partner engagement.</span></span>  |

### <a name="status-and-substatus-transition-states"></a><span data-ttu-id="801f7-183">Állapot-és alállapot-áttérési állapotok</span><span class="sxs-lookup"><span data-stu-id="801f7-183">Status and substatus transition states</span></span>

| <span data-ttu-id="801f7-184">Állapot</span><span class="sxs-lookup"><span data-stu-id="801f7-184">Status</span></span> | <span data-ttu-id="801f7-185">Engedélyezett állapot-váltás</span><span class="sxs-lookup"><span data-stu-id="801f7-185">Allowed Status Transition</span></span> | <span data-ttu-id="801f7-186">Engedélyezett alállapot</span><span class="sxs-lookup"><span data-stu-id="801f7-186">Allowed Substatus</span></span>            |
|--------|---------------------------|------------------------------|
| <span data-ttu-id="801f7-187">Új</span><span class="sxs-lookup"><span data-stu-id="801f7-187">New</span></span>    | <span data-ttu-id="801f7-188">Új, aktív, lezárt</span><span class="sxs-lookup"><span data-stu-id="801f7-188">New, Active, Closed</span></span>       | <span data-ttu-id="801f7-189">Függőben, fogadva</span><span class="sxs-lookup"><span data-stu-id="801f7-189">Pending, Received</span></span>            |
| <span data-ttu-id="801f7-190">Aktív</span><span class="sxs-lookup"><span data-stu-id="801f7-190">Active</span></span> | <span data-ttu-id="801f7-191">Aktív, lezárt</span><span class="sxs-lookup"><span data-stu-id="801f7-191">Active, Closed</span></span>            | <span data-ttu-id="801f7-192">Elfogadva</span><span class="sxs-lookup"><span data-stu-id="801f7-192">Accepted</span></span>                     |
| <span data-ttu-id="801f7-193">Lezárt</span><span class="sxs-lookup"><span data-stu-id="801f7-193">Closed</span></span> | <span data-ttu-id="801f7-194">Lezárt</span><span class="sxs-lookup"><span data-stu-id="801f7-194">Closed</span></span>                    | <span data-ttu-id="801f7-195">Megnyert, elveszett, visszautasított, lejárt</span><span class="sxs-lookup"><span data-stu-id="801f7-195">Won, Lost, Declined, Expired</span></span> |

### <a name="request-example"></a><span data-ttu-id="801f7-196">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="801f7-196">Request example</span></span>

```http
PUT https://api.partner.microsoft.com/v1.0/engagements/referrals/49d90c72-3326-4f61-aacc-2cb57970448c HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

 {
    "id": "49d90c72-3326-4f61-aacc-2cb57970448c",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "createdDateTime": "2018-11-06T18:40:42.6178337Z",
    "updatedDateTime": "2018-11-06T18:40:42.6178337Z",
    "expirationDateTime": "2018-11-14T00:00:00Z",
    "status": "Closed",
    "substatus": "Won",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Independent",
    "target": [
        {
            "type": "BusinessProfileLocation",
            "id": "01e2abcd-52b0-4af3-a3ae-1fd1530b3563"
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
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\"",

}
```

> [!IMPORTANT]
> <span data-ttu-id="801f7-197">Távolítsa el az `"links": { }` objektumot az Put erőforrásból.</span><span class="sxs-lookup"><span data-stu-id="801f7-197">Remove the `"links": { }` object from the PUT resource.</span></span>

## <a name="rest-response"></a><span data-ttu-id="801f7-198">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="801f7-198">REST Response</span></span>

<span data-ttu-id="801f7-199">Ha ez sikeres, ez a metódus a válasz törzsében lévő felszámított [hivatkozó](referral-resources.md) erőforrást adja vissza.</span><span class="sxs-lookup"><span data-stu-id="801f7-199">If successful, this method returns the populated [referral](referral-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="801f7-200">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="801f7-200">Response success and error codes</span></span>

<span data-ttu-id="801f7-201">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="801f7-201">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="801f7-202">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="801f7-202">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="801f7-203">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="801f7-203">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="801f7-204">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="801f7-204">Response example</span></span>

``` http
{
    "id": "4111fffc-f9ee-4d53-bba6-569135228642",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Contoso Company",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "createdDateTime": "2018-11-06T18:40:42.6178337Z",
    "updatedDateTime": "2018-11-06T18:43:38.9948636Z",
    "expirationDateTime": "2018-11-14T00:00:00Z",
    "status": "Closed",
    "substatus": "Won",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Independent",
    "target": [
        {
            "type": "BusinessProfileLocation",
            "id": "01e2abcd-52b0-4af3-a3ae-1fd1530b3563"
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
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\"",
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