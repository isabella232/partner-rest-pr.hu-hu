---
title: Az érdeklődők programozott módon kezelhetők és közös értékesítési lehetőségek a partner Centerben
description: Ez a szakasz azt ismerteti, hogy a partnerek hogyan használhatják a partner API-kat, hogy programozott módon kezeljék az érdeklődőket és a közös értékesítési lehetőségeket.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0da725c9b2459a6c5631b7cc7e21b46e9a7191b8
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770536"
---
# <a name="programmatically-manage-leads-and-co-sell-opportunities-in-partner-center"></a><span data-ttu-id="885d5-103">Az érdeklődők programozott módon kezelhetők és közös értékesítési lehetőségek a partner Centerben</span><span class="sxs-lookup"><span data-stu-id="885d5-103">Programmatically manage leads and co-sell opportunities in Partner Center</span></span>

<span data-ttu-id="885d5-104">Ez a cikk segít megismerni, hogyan felügyelheti a Microsoft-megoldások szolgáltatójának oldaláról kapott érdeklődőket, valamint a Microsoft értékesítési képviselőjétől vagy más partnereinktől kapott közös értékesítési lehetőségeket.</span><span class="sxs-lookup"><span data-stu-id="885d5-104">This article will help you understand how you can programmatically manage the leads that you receive from Microsoft solution provider page and the co-sell opportunities that you receive from Microsoft sales representative or other partners.</span></span> <span data-ttu-id="885d5-105">Ezen API-k használatával programozott módon megoszthatja a vállalat értékesítési folyamatát, vagy meghívhatja a Microsoft értékesítési képviselőit, hogy működjenek együtt a lehetséges lehetőségekkel.</span><span class="sxs-lookup"><span data-stu-id="885d5-105">You can also use these api's to programmatically share your company's sales pipeline or invite Microsoft sales representatives to collaborate on potential opportunities.</span></span> 

## <a name="manage-leads-and-opportunities"></a><span data-ttu-id="885d5-106">Érdeklődők és lehetőségek kezelése</span><span class="sxs-lookup"><span data-stu-id="885d5-106">Manage leads and opportunities</span></span>

- <span data-ttu-id="885d5-107">[Az érdeklődők és lehetőségek listájának beszerzése – beolvassa](get-a-list-of-referrals.md) a Microsoft megoldás-szolgáltató oldaláról származó érdeklődők listáját, és a Microsoft Sellers vagy más partnerek közös értékesítési lehetőségeit.</span><span class="sxs-lookup"><span data-stu-id="885d5-107">[Get the list of leads and opportunities](get-a-list-of-referrals.md) - Gets the list of leads from Microsoft solution provider page and co-sell opportunities from Microsoft sellers or other partners.</span></span> <span data-ttu-id="885d5-108">Ez tartalmazza a szervezete által létrehozott lehetőségek listáját is.</span><span class="sxs-lookup"><span data-stu-id="885d5-108">This will also contain the list of opportunities created by your organization.</span></span>
- <span data-ttu-id="885d5-109">[Érdeklődő vagy lehetőség beszerzése azonosító alapján](get-a-referral-by-Id.md) – az azonosító alapján egy érdeklődőt vagy lehetőséget kap.</span><span class="sxs-lookup"><span data-stu-id="885d5-109">[Get a lead or opportunity by Id](get-a-referral-by-Id.md) - Gets a lead or opportunity by Id.</span></span>
- <span data-ttu-id="885d5-110">[Érdeklődő vagy lehetőség frissítése](patch-a-referral.md) – lehetővé teszi, hogy frissítse az érdeklődők vagy a lehetőségek részleteit, például az ügylet értékét, a becsült zárási dátumot, illetve az értékesítési fázisok további részletek közötti kezelését.</span><span class="sxs-lookup"><span data-stu-id="885d5-110">[Update a lead or opportunity](patch-a-referral.md) - Allows you to update the lead or opportunity details like the deal value, estimated close date or manage the sales stages amongst other details.</span></span>
- <span data-ttu-id="885d5-111">[Új lehetőség létrehozása](create-a-referral.md) – lehetővé teszi egy új közös értékesítési lehetőség vagy privát üzlet létrehozását.</span><span class="sxs-lookup"><span data-stu-id="885d5-111">[Create a new opportunity](create-a-referral.md) - Enables you to create a new co-sell opportunity or private deal.</span></span>
- [<span data-ttu-id="885d5-112">Javaslati erőforrások</span><span class="sxs-lookup"><span data-stu-id="885d5-112">Referral resources</span></span>](referral-resources.md)

> [!Note]
> <span data-ttu-id="885d5-113">A Microsoft kereskedelmi piactérről (Azure Marketplace és AppSource) kapott érdeklődők nem kezelhetők a partner Center API-k használatával.</span><span class="sxs-lookup"><span data-stu-id="885d5-113">Leads received from the Microsoft commercial marketplace (Azure Marketplace and AppSource) cannot be managed using Partner Center api's.</span></span>