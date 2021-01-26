---
title: Partner API hitelesítése
description: Konfigurálja a hitelesítési beállításokat úgy, hogy a partner API-t használja az Azure AD-vel a hitelesítéshez.
ms.date: 05/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: c5810678dccc2be1c3c084c901299961d6ba7820
ms.sourcegitcommit: 3c165938f544ff226cbe11ca21ed5aa00448d9b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2020
ms.locfileid: "97770501"
---
# <a name="partner-api-authentication"></a><span data-ttu-id="e54e3-103">Partner API hitelesítése</span><span class="sxs-lookup"><span data-stu-id="e54e3-103">Partner API authentication</span></span>

<span data-ttu-id="e54e3-104">A következőkre vonatkozik:</span><span class="sxs-lookup"><span data-stu-id="e54e3-104">Applies to:</span></span>

- <span data-ttu-id="e54e3-105">Partner API</span><span class="sxs-lookup"><span data-stu-id="e54e3-105">Partner API</span></span>

<span data-ttu-id="e54e3-106">A partner API a Azure Active Directoryt (Azure AD) használja a hitelesítéshez.</span><span class="sxs-lookup"><span data-stu-id="e54e3-106">The Partner API utilizes Azure Active Directory (Azure AD) for authentication.</span></span> <span data-ttu-id="e54e3-107">Ha együttműködik a partner API-val, megfelelően konfigurálnia kell egy Azure AD-alkalmazást, és be kell szereznie egy hozzáférési jogkivonatot.</span><span class="sxs-lookup"><span data-stu-id="e54e3-107">When you interact with the Partner API, you must correctly configure an Azure AD application and obtain an access token.</span></span> <span data-ttu-id="e54e3-108">Hozzáférési jogkivonatokat kérhet az [alkalmazás-és felhasználói hozzáféréshez](#application-and-user-access) , vagy [csak az alkalmazáshoz való hozzáférést](#application-only-access).</span><span class="sxs-lookup"><span data-stu-id="e54e3-108">You can obtain access tokens for [application and user access](#application-and-user-access) or [application-only access](#application-only-access).</span></span>

## <a name="application-and-user-access"></a><span data-ttu-id="e54e3-109">Alkalmazás-és felhasználói hozzáférés</span><span class="sxs-lookup"><span data-stu-id="e54e3-109">Application and user access</span></span>

<span data-ttu-id="e54e3-110">Ez a módszer ajánlott az **alkalmazás-és felhasználói hozzáférés** beállításához az API-hoz.</span><span class="sxs-lookup"><span data-stu-id="e54e3-110">This method is recommended to set up **application and user access** to the API.</span></span>

1. <span data-ttu-id="e54e3-111">Jelentkezzen be az [Azure Portalra](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e54e3-111">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e54e3-112">Válassza ki a **Azure Active Directory** szolgáltatást.</span><span class="sxs-lookup"><span data-stu-id="e54e3-112">Choose the **Azure Active Directory** service.</span></span>
3. <span data-ttu-id="e54e3-113">Válassza a **Alkalmazásregisztrációk**, majd az **új alkalmazás regisztrálása** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="e54e3-113">Choose **App registrations**, then choose **New application registration**.</span></span>
4. <span data-ttu-id="e54e3-114">Hozza létre az új alkalmazást.</span><span class="sxs-lookup"><span data-stu-id="e54e3-114">Create your new application.</span></span> <span data-ttu-id="e54e3-115">Az **alkalmazás típusa** mezőben válassza a **natív** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="e54e3-115">For **Application type**, select **Native**.</span></span> <span data-ttu-id="e54e3-116">Adjon meg egy nevet és egy URL-címet, majd válassza a **Létrehozás** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="e54e3-116">Provide a name and URL, then select **Create**.</span></span>
5. <span data-ttu-id="e54e3-117">Válassza ki az alkalmazás **API-engedélyeit** .</span><span class="sxs-lookup"><span data-stu-id="e54e3-117">Choose **API permissions** for the application.</span></span> <span data-ttu-id="e54e3-118">Az **API-engedélyek kérése** képernyőn válassza az **engedély hozzáadása**, majd a **szervezet által használt API** -k elemet.</span><span class="sxs-lookup"><span data-stu-id="e54e3-118">On the **Request API permissions** screen, choose **Add a permission**, then choose **APIs my organization uses**</span></span>
6. <span data-ttu-id="e54e3-119">Keressen rá a *Microsoft partner* (*Microsoft dev Center*) API ( `4990cffe-04e8-4e8b-808a-1175604b879f` ) kifejezésre.</span><span class="sxs-lookup"><span data-stu-id="e54e3-119">Search for the *Microsoft Partner* (*Microsoft Dev Center*) API (`4990cffe-04e8-4e8b-808a-1175604b879f`).</span></span>

    ![Képernyőkép a kérelem API-engedélyeiről képernyőről a Microsoft partner API-val való kereséssel](../images/SearchGatewayApi.png)

7. <span data-ttu-id="e54e3-121">Állítsa be a **delegált engedélyeket** a **partner központba**.</span><span class="sxs-lookup"><span data-stu-id="e54e3-121">Set the **Delegated Permissions** to **Partner Center**.</span></span>

    ![Képernyőkép a delegált engedélyek konfigurációs képernyőjéről a Microsoft partner API-hoz](../images/SelectUserPermission.png)
    
8. <span data-ttu-id="e54e3-123">Keressen rá a *Microsoft partner* (*Microsoft partner Center*) API ( `fa3d9a0c-3fb0-42cc-9193-47c7ecd2edbd` ) kifejezésre.</span><span class="sxs-lookup"><span data-stu-id="e54e3-123">Search for the *Microsoft Partner* (*Microsoft Partner Center*) API (`fa3d9a0c-3fb0-42cc-9193-47c7ecd2edbd`).</span></span>

    ![Képernyőkép a kérelmek API-engedélyeiről képernyőről a Microsoft partner Center API-val való kereséssel](../images/SearchPCApi.png)
    
9. <span data-ttu-id="e54e3-125">Válassza ki a **Microsoft partner centert** , és jelölje be a **user_impersonation**.</span><span class="sxs-lookup"><span data-stu-id="e54e3-125">Select **Microsoft Partner Center** and check **user_impersonation**.</span></span>

10. <span data-ttu-id="e54e3-126">Állítsa be a **delegált engedélyeket** a **partner központba**.</span><span class="sxs-lookup"><span data-stu-id="e54e3-126">Set the **Delegated Permissions** to **Partner Center**.</span></span>

    ![Képernyőkép a delegált engedélyek konfigurációs képernyőjéről a Microsoft partner Center API-hoz](../images/SelectPCUserPermission.png)

## <a name="application-only-access"></a><span data-ttu-id="e54e3-128">Csak alkalmazáshoz való hozzáférés</span><span class="sxs-lookup"><span data-stu-id="e54e3-128">Application-only access</span></span>

<span data-ttu-id="e54e3-129">Ez a metódus csak az API **-khoz való alkalmazás-hozzáférés** beállításához ajánlott.</span><span class="sxs-lookup"><span data-stu-id="e54e3-129">This method is recommended for **application-only access** setup to the APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e54e3-130">Meg kell adnia az alkalmazás AZONOSÍTÓját, az alkalmazás kulcsát és a címtár AZONOSÍTÓját az Azure AD-alkalmazásból.</span><span class="sxs-lookup"><span data-stu-id="e54e3-130">You must provide the application ID, application key, and directory ID from your Azure AD application.</span></span>

1. <span data-ttu-id="e54e3-131">Jelentkezzen be az [Azure Portalra](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e54e3-131">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e54e3-132">Válassza ki a **Azure Active Directory** szolgáltatást.</span><span class="sxs-lookup"><span data-stu-id="e54e3-132">Select the **Azure Active Directory** service.</span></span>
3. <span data-ttu-id="e54e3-133">Válassza a **Alkalmazásregisztrációk** lehetőséget, majd válassza az **új alkalmazás regisztrálása** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="e54e3-133">Choose **App registrations**, then select **New application registration**.</span></span>
4. <span data-ttu-id="e54e3-134">Hozza létre az új alkalmazást.</span><span class="sxs-lookup"><span data-stu-id="e54e3-134">Create your new application.</span></span> <span data-ttu-id="e54e3-135">Az **alkalmazás típusa mezőben** válassza a **Web App/API** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="e54e3-135">For **Application type**, choose **Web app/API**.</span></span> <span data-ttu-id="e54e3-136">Adja meg az alkalmazás **nevét** és **URL-címét**.</span><span class="sxs-lookup"><span data-stu-id="e54e3-136">Enter a an application **name** and **URL**.</span></span> <span data-ttu-id="e54e3-137">Ezután válassza a **Létrehozás** elemet.</span><span class="sxs-lookup"><span data-stu-id="e54e3-137">Then choose **Create**.</span></span>
5. <span data-ttu-id="e54e3-138">Válassza ki az alkalmazás **API-engedélyeit** .</span><span class="sxs-lookup"><span data-stu-id="e54e3-138">Choose **API permissions** for the application.</span></span> <span data-ttu-id="e54e3-139">Válassza az **engedély hozzáadása** lehetőséget, majd **a saját szervezet által használt API** -k elemet.</span><span class="sxs-lookup"><span data-stu-id="e54e3-139">Choose **Add a permission**, then choose **APIs my organization uses**</span></span>
6. <span data-ttu-id="e54e3-140">Keressen rá a *Microsoft partner* (*Microsoft dev Center*) API ( `4990cffe-04e8-4e8b-808a-1175604b879f` ) kifejezésre.</span><span class="sxs-lookup"><span data-stu-id="e54e3-140">Search for the *Microsoft Partner* (*Microsoft Dev Center*) API (`4990cffe-04e8-4e8b-808a-1175604b879f`).</span></span>

    ![Képernyőkép a kérelem API-engedélyeiről képernyőről a Microsoft partner API-val való kereséssel](../images/SearchGatewayApi.png)

7. <span data-ttu-id="e54e3-142">Állítsa be a **delegált engedélyeket** a **partner központba**.</span><span class="sxs-lookup"><span data-stu-id="e54e3-142">Set the **Delegated Permissions** to **Partner Center**.</span></span>

    ![Képernyőkép a delegált engedélyek konfigurációs képernyőjéről a Microsoft partner API-hoz](../images/SelectUserPermission.png)

8. <span data-ttu-id="e54e3-144">A regisztrált alkalmazáshoz válassza a **Tulajdonságok** lehetőséget, majd válassza **az alkalmazás azonosítójának másolása** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="e54e3-144">For the application you registered, choose **Properties** and then select **copy the Application ID**.</span></span>
9. <span data-ttu-id="e54e3-145">Válassza a **Beállítások**, majd a **tanúsítványok & Secrets** elemet.</span><span class="sxs-lookup"><span data-stu-id="e54e3-145">Choose **Settings**, then choose **Certificates & Secrets**.</span></span> <span data-ttu-id="e54e3-146">Válassza az **új ügyfél titkot** , és állítsa a **lejárat**  lehetőséget, hogy **Soha ne járjon le**.</span><span class="sxs-lookup"><span data-stu-id="e54e3-146">Choose **New Client Secret** and set the **Expiration**  to **Never expires**.</span></span> <span data-ttu-id="e54e3-147">Ezután válassza a **Mentés** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="e54e3-147">Then choose **Save**.</span></span>
10. <span data-ttu-id="e54e3-148">A **kulcsok** menüben válassza **a kulcs értékének másolása** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="e54e3-148">On the **Keys** menu, choose **Copy the key value**.</span></span> <span data-ttu-id="e54e3-149">Mentse az érték másolatát.</span><span class="sxs-lookup"><span data-stu-id="e54e3-149">Save a copy of this value.</span></span>

> [!WARNING]
> <span data-ttu-id="e54e3-150">Ne felejtse el menteni a kulcs értékének másolatát a létrehozott kulcshoz.</span><span class="sxs-lookup"><span data-stu-id="e54e3-150">Be sure to save a copy of the key value for the key you created.</span></span> <span data-ttu-id="e54e3-151">Ezt a kulcs értéket később kell használnia a jogkivonat beszerzéséhez.</span><span class="sxs-lookup"><span data-stu-id="e54e3-151">You will need to use this key value later to obtain a token.</span></span>

## <a name="partner-consent"></a><span data-ttu-id="e54e3-152">Partneri beleegyezett</span><span class="sxs-lookup"><span data-stu-id="e54e3-152">Partner consent</span></span>

<span data-ttu-id="e54e3-153">Az Azure felügyeleti portálján válassza a **vállalati alkalmazások** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="e54e3-153">In the Azure management portal, select **Enterprise applications**.</span></span> <span data-ttu-id="e54e3-154">Keresse meg az előző szakaszban létrehozott alkalmazást, és válassza ki az alkalmazást.</span><span class="sxs-lookup"><span data-stu-id="e54e3-154">Search for the application you created in the previous section, and select that application.</span></span> <span data-ttu-id="e54e3-155">Válassza az **engedélyek** lehetőséget, majd válassza **a rendszergazdai jóváhagyás megadása partner fiókhoz** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="e54e3-155">Select **Permissions** , then select **Grant Admin Consent for Partner Account**.</span></span>
