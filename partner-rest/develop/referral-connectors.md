---
title: Hivatkozó összekötők.
description: A partneri átirányítások szinkronizálása a Dynamics 365 CRM-érdeklődőkkel a Microsoft Flow használatával.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0a62023feb03114bb7ba1136b7700875f24c2e01
ms.sourcegitcommit: 0508b7302a3965fd5537b05c1f0397a1da014257
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/27/2020
ms.locfileid: "97770394"
---
# <a name="referral-connectors"></a><span data-ttu-id="9cc52-103">Hivatkozó összekötők</span><span class="sxs-lookup"><span data-stu-id="9cc52-103">Referral connectors</span></span>

<span data-ttu-id="9cc52-104">Az átirányítási összekötők segítségével szinkronizálhatja a partneri hivatkozásokat az Ügyfélkapcsolat-kezelési (CRM) érdeklődőkkel.</span><span class="sxs-lookup"><span data-stu-id="9cc52-104">You can use referral connectors to synchronize partner referrals with customer relationship management (CRM) leads.</span></span> <span data-ttu-id="9cc52-105">Az átirányítási összekötőt [Microsoft flow](https://flow.microsoft.com) használatával HTTPS-végpontként hozhatja létre a partneri átirányítások fogadásához.</span><span class="sxs-lookup"><span data-stu-id="9cc52-105">You can create a referral connector using [Microsoft Flow](https://flow.microsoft.com) as the HTTPS endpoint to receive partner referrals.</span></span> <span data-ttu-id="9cc52-106">Ezután megírhatja a folyamat által a CRM rendszernek érdeklődőként kapott átirányítást.</span><span class="sxs-lookup"><span data-stu-id="9cc52-106">You can then write the referral received by the flow to a CRM system as a lead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9cc52-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="9cc52-107">Prerequisites</span></span>

* <span data-ttu-id="9cc52-108">Előfizetés Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="9cc52-108">Microsoft Flow subscription</span></span>
  * <span data-ttu-id="9cc52-109">Fiók rendszergazdai hozzáféréssel ehhez az előfizetéshez</span><span class="sxs-lookup"><span data-stu-id="9cc52-109">Account with administrator access to this subscription</span></span>
* <span data-ttu-id="9cc52-110">Azure Active Directory (Azure AD) alkalmazás-azonosító, felhasználói azonosító, jelszó és bérlő azonosítója (a partner API eléréséhez használatos).</span><span class="sxs-lookup"><span data-stu-id="9cc52-110">Azure Active Directory (Azure AD) application ID, user id, password and tenant ID (used to access the Partner API).</span></span> <span data-ttu-id="9cc52-111">A telepítési utasításokért lásd: [partner-hitelesítés](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9cc52-111">For setup instructions, see [Partner authentication](api-authentication.md).</span></span>
* <span data-ttu-id="9cc52-112">[Azure Function app](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) -előfizetés.</span><span class="sxs-lookup"><span data-stu-id="9cc52-112">[Azure function app](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) subscription.</span></span>
* <span data-ttu-id="9cc52-113">A [partneri központ webhook esemény](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events) -előfizetése a [létrehozott](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-created-event) és a [hivatkozó frissített](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-updated-event) eseményekre.</span><span class="sxs-lookup"><span data-stu-id="9cc52-113">[Partner Center webhook event](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events) subscription to [Referral Created](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-created-event) and [Referral Updated](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-updated-event) events.</span></span>
* <span data-ttu-id="9cc52-114">[Microsoft Dynamics 365](https://dynamics.microsoft.com) -előfizetés</span><span class="sxs-lookup"><span data-stu-id="9cc52-114">[Microsoft Dynamics 365](https://dynamics.microsoft.com) subscription</span></span>
  * <span data-ttu-id="9cc52-115">Értékesítési modul engedélyezve</span><span class="sxs-lookup"><span data-stu-id="9cc52-115">Sales module enabled</span></span>
  * <span data-ttu-id="9cc52-116">Fiók rendszergazdai hozzáféréssel ehhez az előfizetéshez</span><span class="sxs-lookup"><span data-stu-id="9cc52-116">Account with administrator access to this subscription</span></span>

## <a name="flow-overview"></a><span data-ttu-id="9cc52-117">A flow áttekintése</span><span class="sxs-lookup"><span data-stu-id="9cc52-117">Flow overview</span></span>

<span data-ttu-id="9cc52-118">Az átirányítások importálása a CRM-be a következő folyamat használatával történik:</span><span class="sxs-lookup"><span data-stu-id="9cc52-118">Referrals are imported into the CRM using the following flow:</span></span>

1. <span data-ttu-id="9cc52-119">A partner egy webhookot állít be az átirányítási értesítések fogadásához.</span><span class="sxs-lookup"><span data-stu-id="9cc52-119">Partner sets up a webhook to receive referral notifications.</span></span>
2. <span data-ttu-id="9cc52-120">A partner regisztrálja a webhookot a partner centerrel.</span><span class="sxs-lookup"><span data-stu-id="9cc52-120">Partner registers the webhook with Partner Center.</span></span> <span data-ttu-id="9cc52-121">A partner arra is előfizet, hogy mikor hozza létre vagy frissíti a webhook eseményeit.</span><span class="sxs-lookup"><span data-stu-id="9cc52-121">The partner also subscribes to webhook events for when referrals are created or updated.</span></span>
3. <span data-ttu-id="9cc52-122">Az Ajánlói ügyfél létrehoz vagy frissít egy átirányítást.</span><span class="sxs-lookup"><span data-stu-id="9cc52-122">Referral client creates or updates a referral.</span></span>
4. <span data-ttu-id="9cc52-123">A partner Center webhook rendszer ellenőrzi a partner regisztrációját, és értesítést küld a webhooknak.</span><span class="sxs-lookup"><span data-stu-id="9cc52-123">Partner Center webhook system checks for the partner's registration and sends a notification to the webhook.</span></span>
5. <span data-ttu-id="9cc52-124">A webhook megkapja az értesítést.</span><span class="sxs-lookup"><span data-stu-id="9cc52-124">Webhook receives the notification.</span></span>
6. <span data-ttu-id="9cc52-125">A Microsoft flow-ban található flow-dokumentum tokent használ a partner Center Referral API meghívásához.</span><span class="sxs-lookup"><span data-stu-id="9cc52-125">Flow document in Microsoft flow uses a token to make a call to the Partner Center referral API.</span></span>
7. <span data-ttu-id="9cc52-126">A flow-végpont megkapja az átirányítást.</span><span class="sxs-lookup"><span data-stu-id="9cc52-126">Flow endpoint gets the referral.</span></span>
8. <span data-ttu-id="9cc52-127">A flow-végpont létrehozza a CRM-érdeklődőt.</span><span class="sxs-lookup"><span data-stu-id="9cc52-127">Flow endpoint creates the CRM lead.</span></span>

![Az ebben a szakaszban ismertetett lépéseket a partnerek CRM-be történő importálásának folyamata című szakasz mutatja.](../images/referralwebhook.png)

## <a name="flow-document-process"></a><span data-ttu-id="9cc52-129">Flow-dokumentum folyamata</span><span class="sxs-lookup"><span data-stu-id="9cc52-129">Flow document process</span></span>

<span data-ttu-id="9cc52-130">Az átirányítási összekötőhöz tartozó flow-dokumentum a Dynamics 365-ből származó CRM-érdeklődővel szinkronizál egy partneri hivatkozást.</span><span class="sxs-lookup"><span data-stu-id="9cc52-130">The flow document for a referral connector synchronizes a partner referral with a CRM lead from Dynamics 365.</span></span>

1. <span data-ttu-id="9cc52-131">Az összekötő lekérdezi a csatlakozáshoz szükséges tokent `https://api.partner.microsoft.com/v1.0/engagements/referrals` .</span><span class="sxs-lookup"><span data-stu-id="9cc52-131">Connector gets a token to connect to `https://api.partner.microsoft.com/v1.0/engagements/referrals`.</span></span>
2. <span data-ttu-id="9cc52-132">Az összekötő beolvassa az összekötőt a használatával indító hivatkozással `https://api.partner.microsoft.com/v1.0/engagements/referrals/{id}` .</span><span class="sxs-lookup"><span data-stu-id="9cc52-132">Connector obtains referral that triggered the connector using `https://api.partner.microsoft.com/v1.0/engagements/referrals/{id}`.</span></span>
3. <span data-ttu-id="9cc52-133">Az összekötő a Dynamics 365-hoz csatlakozik.</span><span class="sxs-lookup"><span data-stu-id="9cc52-133">Connector connects to Dynamics 365.</span></span>
4. <span data-ttu-id="9cc52-134">Az összekötő létrehoz egy új érdeklődőt, vagy frissít egy meglévő érdeklődőt az átirányítással kapcsolatos legfrissebb információkkal.</span><span class="sxs-lookup"><span data-stu-id="9cc52-134">Connector creates a new lead or updates an existing lead with the latest information on the referral.</span></span>
5. <span data-ttu-id="9cc52-135">Az összekötő frissítései a CRM-érdeklődő legújabb frissítéseire hivatkoznak.</span><span class="sxs-lookup"><span data-stu-id="9cc52-135">Connector updates referral with the latest updates from the CRM lead.</span></span>

![Az ebben a szakaszban szereplő lépéseket bemutató folyamatábra.](../images/ReferralFlowSteps.png)

## <a name="sample-referral-connector"></a><span data-ttu-id="9cc52-137">Példa Ajánlói összekötő</span><span class="sxs-lookup"><span data-stu-id="9cc52-137">Sample referral connector</span></span>

<span data-ttu-id="9cc52-138">A következő *minta-átirányítási összekötő* bemutatja, hogyan szinkronizálhat a partner Center-hivatkozásokat a CRM-érdeklődők számára a Dynamics 365-ben.</span><span class="sxs-lookup"><span data-stu-id="9cc52-138">The following *sample referral connector* shows how to synchronize Partner Center referrals to CRM leads in Dynamics 365.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9cc52-139">Más CRM is írhat, ha a minta kódjában lecseréli a [flow-összekötőket](https://flow.microsoft.com/en-us/connectors/) .</span><span class="sxs-lookup"><span data-stu-id="9cc52-139">You can write to different CRMs by replacing the [flow connectors](https://flow.microsoft.com/en-us/connectors/) in the sample code.</span></span>

### <a name="import-flow-synchronization-package"></a><span data-ttu-id="9cc52-140">Adatfolyam-szinkronizálási csomag importálása</span><span class="sxs-lookup"><span data-stu-id="9cc52-140">Import flow synchronization package</span></span>

<span data-ttu-id="9cc52-141">Töltse le és importálja a *mintakód-csomagot* a Microsoft Flowba, és kapcsolódjon a Dynamics 365-hez:</span><span class="sxs-lookup"><span data-stu-id="9cc52-141">Download and import the *sample code package* into Microsoft Flow and connect to Dynamics 365:</span></span>

1. <span data-ttu-id="9cc52-142">Töltse le a [flow szinkronizációs csomagot](https://github.com/microsoft/Partner-Center-Referrals/blob/master/flowconnectors/MicrosoftDynamicsCRM/PartnerReferralsToDynamicsCRMLead.zip?raw=true) a [GitHub](https://github.com/microsoft/Partner-Center-Referrals)-adattárból.</span><span class="sxs-lookup"><span data-stu-id="9cc52-142">Download the [flow synchronization package](https://github.com/microsoft/Partner-Center-Referrals/blob/master/flowconnectors/MicrosoftDynamicsCRM/PartnerReferralsToDynamicsCRMLead.zip?raw=true) from the [GitHub repo](https://github.com/microsoft/Partner-Center-Referrals).</span></span>
2. <span data-ttu-id="9cc52-143">A megfelelő hitelesítő adatok használatával jelentkezzen be [Microsoft flow](https://flow.microsoft.com) .</span><span class="sxs-lookup"><span data-stu-id="9cc52-143">Sign in to [Microsoft Flow](https://flow.microsoft.com) using the appropriate credentials.</span></span>
3. <span data-ttu-id="9cc52-144">Válassza a **saját folyamatok** lehetőséget a navigációs menüben.</span><span class="sxs-lookup"><span data-stu-id="9cc52-144">Choose **My Flows** in the navigation menu.</span></span> <span data-ttu-id="9cc52-145">Ezután válassza az **Importálás** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="9cc52-145">Then choose **Import**.</span></span>
4. <span data-ttu-id="9cc52-146">A **csomag importálása** lapon válassza ki a letöltött flow szinkronizációs csomagot.</span><span class="sxs-lookup"><span data-stu-id="9cc52-146">On the **Import package** page, select the flow synchronization package that you downloaded.</span></span> <span data-ttu-id="9cc52-147">Ezután válassza a **feltöltés** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="9cc52-147">Then choose **Upload**.</span></span>

    ![Csomag importálása képernyő](../images/importPackage.png)

5. <span data-ttu-id="9cc52-149">A csomag feltöltésének befejezése után keresse meg a csomag **tartalmának áttekintése** lapon feltöltött csomagot.</span><span class="sxs-lookup"><span data-stu-id="9cc52-149">After the package upload is complete, find the package you uploaded in the **Review Package Content** .</span></span>

    ![A csomag importálása képernyő részletei](../images/importPackageDetails.png)

6. <span data-ttu-id="9cc52-151">Válassza a **művelet** gombot (ceruza ikon) a feltöltött csomaghoz.</span><span class="sxs-lookup"><span data-stu-id="9cc52-151">Choose the **Action** button (pencil icon) for your uploaded package.</span></span> <span data-ttu-id="9cc52-152">Ekkor megnyílik a **telepítő importálása** panel.</span><span class="sxs-lookup"><span data-stu-id="9cc52-152">This opens the **Import setup** blade.</span></span>
7. <span data-ttu-id="9cc52-153">Válassza ki a **telepítési** típust.</span><span class="sxs-lookup"><span data-stu-id="9cc52-153">Choose your **Setup** type.</span></span>

    * <span data-ttu-id="9cc52-154">Új folyamat létrehozásához válassza a **Létrehozás új néven** lehetőséget, majd adjon meg egy új **nevet**.</span><span class="sxs-lookup"><span data-stu-id="9cc52-154">To create a new flow, select **Create as new**, and enter a new **Resource name**.</span></span>
    * <span data-ttu-id="9cc52-155">Ha egy meglévő folyamatot ugyanazzal a névvel szeretne frissíteni, válassza a **frissítés** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="9cc52-155">To update an existing flow with the same name, select **Update**.</span></span>

    ![Új csomagjának felvétele-képernyő létrehozása vagy frissítése](../images/CreateNewConnection.png)

8. <span data-ttu-id="9cc52-157">A **csomag importálása** oldalon keresse meg a Dynamics 365-kapcsolatát a **kapcsolódó erőforrások** szakasz **Tartalom áttekintése** szakaszában.</span><span class="sxs-lookup"><span data-stu-id="9cc52-157">On the **Import package** page, find your Dynamics 365 connection in the **Review Package Content** section under **Related Resources**.</span></span>
9. <span data-ttu-id="9cc52-158">Válassza a **művelet** gombot (ceruza ikon) a Dynamics 365-kapcsolathoz.</span><span class="sxs-lookup"><span data-stu-id="9cc52-158">Choose the **Action** button (pencil icon) for your Dynamics 365 connection.</span></span> <span data-ttu-id="9cc52-159">Ekkor megnyílik a kapcsolódó erőforrás **Importálás beállítása** panelje.</span><span class="sxs-lookup"><span data-stu-id="9cc52-159">This opens the **Import setup** blade for this related resource.</span></span>
10. <span data-ttu-id="9cc52-160">Válassza az **új létrehozása** elemet, és hozzon létre egy új Dynamics 365-kapcsolatokat, vagy válasszon ki egy meglévőt.</span><span class="sxs-lookup"><span data-stu-id="9cc52-160">Choose **Create new** to create a new Dynamics 365 connection, or select an existing connection.</span></span>
11. <span data-ttu-id="9cc52-161">Győződjön meg arról, hogy a **csomag importálása** lap most megjeleníti a kiválasztott flow-telepítési típust és a Dynamics 365-kapcsolatokat.</span><span class="sxs-lookup"><span data-stu-id="9cc52-161">Verify that the **Import package** page now shows your selected flow setup type and Dynamics 365 connection.</span></span> <span data-ttu-id="9cc52-162">Ezután válassza az **Importálás** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="9cc52-162">Then choose **Import**.</span></span>

    ![Csomag állapotának importálása képernyő](../images/importStatus.png)

12. <span data-ttu-id="9cc52-164">Győződjön meg arról, hogy a flow-erőforrás létrehozása vagy frissítése megtörtént.</span><span class="sxs-lookup"><span data-stu-id="9cc52-164">Verify that your flow resource is now created or updated.</span></span>

### <a name="configure-flow-parameters"></a><span data-ttu-id="9cc52-165">Folyamat paramétereinek konfigurálása</span><span class="sxs-lookup"><span data-stu-id="9cc52-165">Configure flow parameters</span></span>

<span data-ttu-id="9cc52-166">Adja meg a flow-erőforrás paramétereit:</span><span class="sxs-lookup"><span data-stu-id="9cc52-166">Configure the parameters of your flow resource:</span></span>

1. <span data-ttu-id="9cc52-167">[Microsoft flow](https://flow.microsoft.com)a navigációs menüben válassza a **saját folyamatok** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="9cc52-167">In [Microsoft Flow](https://flow.microsoft.com), choose **My Flows** in the navigation menu.</span></span>
2. <span data-ttu-id="9cc52-168">Válassza ki az előző szakaszban létrehozott vagy frissített folyamat-erőforrást.</span><span class="sxs-lookup"><span data-stu-id="9cc52-168">Choose the flow resource you created or updated in the previous section.</span></span>
3. <span data-ttu-id="9cc52-169">A folyamat lapon válassza a **folyamat szerkesztése** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="9cc52-169">On the flow page, choose **Edit flow**.</span></span>
4. <span data-ttu-id="9cc52-170">Válassza ki az **HRE-(ügyfél-) azonosító** változót, és adja meg az Azure ad-alkalmazás azonosítóját.</span><span class="sxs-lookup"><span data-stu-id="9cc52-170">Choose the **AAD-Application (client) ID** variable and enter the ID of your Azure AD application.</span></span>
5. <span data-ttu-id="9cc52-171">Válassza ki a **userid** változót, és adja meg a felhasználói azonosítóját.</span><span class="sxs-lookup"><span data-stu-id="9cc52-171">Choose the **UserId** variable and enter your user ID.</span></span>
6. <span data-ttu-id="9cc52-172">Válassza ki a **userPassword** változót, és adja meg a felhasználói jelszavát.</span><span class="sxs-lookup"><span data-stu-id="9cc52-172">Choose the **UserPassword** variable and enter your user password.</span></span>
7. <span data-ttu-id="9cc52-173">Válassza ki a **HRE-Directory (bérlő) azonosító** változót.</span><span class="sxs-lookup"><span data-stu-id="9cc52-173">Select the **AAD-Directory (tenant) ID** variable.</span></span> <span data-ttu-id="9cc52-174">Adja meg az Azure AD-alkalmazás bérlői AZONOSÍTÓját.</span><span class="sxs-lookup"><span data-stu-id="9cc52-174">Enter the tenant ID of your Azure AD application.</span></span>
8. <span data-ttu-id="9cc52-175">Válassza a **Mentés** lehetőséget a folyamat mentéséhez.</span><span class="sxs-lookup"><span data-stu-id="9cc52-175">Choose **Save** to save your flow.</span></span>

    ![Flow változók beállításai képernyő](../images/SetFlowVariables.png)

### <a name="authenticate-the-callback"></a><span data-ttu-id="9cc52-177">A visszahívás hitelesítése</span><span class="sxs-lookup"><span data-stu-id="9cc52-177">Authenticate the callback</span></span>

<span data-ttu-id="9cc52-178">Hitelesítse a visszahívási eseményt a partner központjától:</span><span class="sxs-lookup"><span data-stu-id="9cc52-178">Authenticate the callback event from the Partner Center:</span></span>

> [!TIP]
> <span data-ttu-id="9cc52-179">Példaként tekintse meg a [minta Function alkalmazás kódját](#sample-function-app-code) a következő szakaszban.</span><span class="sxs-lookup"><span data-stu-id="9cc52-179">For an example, see the [sample function app code](#sample-function-app-code) in the following section.</span></span>

1. <span data-ttu-id="9cc52-180">[Hozzon létre egy Azure Function-alkalmazást](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) , amely [hitelesíti a visszahívási eseményt a partner Centertől](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#how-to-authenticate-the-callback).</span><span class="sxs-lookup"><span data-stu-id="9cc52-180">[Create an Azure function app](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) that [authenticates the callback event from the Partner Center](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#how-to-authenticate-the-callback).</span></span>

    1. <span data-ttu-id="9cc52-181">Győződjön meg arról, hogy a szükséges fejlécek jelen vannak (**Authorization**, **x-MS-Certificate-URL** és **x-MS-Signature-algoritmus**).</span><span class="sxs-lookup"><span data-stu-id="9cc52-181">Verify that the required headers are present (**Authorization**, **x-ms-certificate-url**, and **x-ms-signature-algorithm**).</span></span>
    2. <span data-ttu-id="9cc52-182">Töltse le a tartalom aláírásához használt tanúsítványt (**x-MS-Certificate-URL**).</span><span class="sxs-lookup"><span data-stu-id="9cc52-182">Download the certificate used to sign the content (**x-ms-certificate-url**).</span></span>
    3. <span data-ttu-id="9cc52-183">Ellenőrizze a tanúsítványlánc utasításait.</span><span class="sxs-lookup"><span data-stu-id="9cc52-183">Verify the certificate chain.</span></span>
    4. <span data-ttu-id="9cc52-184">Ellenőrizze a tanúsítvány **szervezetét** .</span><span class="sxs-lookup"><span data-stu-id="9cc52-184">Verify the **Organization** of the certificate.</span></span>
    5. <span data-ttu-id="9cc52-185">Az UTF-8 kódolású tartalom beolvasása pufferbe.</span><span class="sxs-lookup"><span data-stu-id="9cc52-185">Read the content with UTF-8 encoding into a buffer.</span></span>
    6. <span data-ttu-id="9cc52-186">Hozzon létre egy RSA titkosítási szolgáltatót.</span><span class="sxs-lookup"><span data-stu-id="9cc52-186">Create an RSA Crypto Provider.</span></span>
    7. <span data-ttu-id="9cc52-187">[Ellenőrizze, hogy az aláírás egyezik-e](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#example-for-signature-validation) a megadott kivonatoló algoritmussal (például sha256).</span><span class="sxs-lookup"><span data-stu-id="9cc52-187">[Verify that the signature matches](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#example-for-signature-validation) what was signed with the specified hash algorithm (for example, SHA256).</span></span>
    8. <span data-ttu-id="9cc52-188">Ha az ellenőrzés sikeres, a rendszer egy **OK** üzenetet ad vissza.</span><span class="sxs-lookup"><span data-stu-id="9cc52-188">If the verification succeeds, an **OK** message is returned.</span></span>

2. <span data-ttu-id="9cc52-189">Figyelje meg a Function app HTTP-végpontjának generált visszahívási URI azonosítóját.</span><span class="sxs-lookup"><span data-stu-id="9cc52-189">Note the generated callback URI for your function app's HTTP endpoint.</span></span> <span data-ttu-id="9cc52-190">Ez az URI a Function alkalmazás létrehozásakor jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="9cc52-190">This URI is displayed when you create your function app.</span></span> <span data-ttu-id="9cc52-191">Ezt az URI-t a Function alkalmazás Azure Resource lapján is megtalálhatja.</span><span class="sxs-lookup"><span data-stu-id="9cc52-191">You can also find this URI on your function app's Azure resource page.</span></span>
3. <span data-ttu-id="9cc52-192">A [Microsoft Flowban](https://flow.microsoft.com)szerkessze a "partneri javaslat a Microsoft Dynamics CRM-vezetőhöz" című szakaszt, amelyet az *[importálási folyamat szinkronizációs csomagja](#import-flow-synchronization-package)* című szakaszban importált.</span><span class="sxs-lookup"><span data-stu-id="9cc52-192">In [Microsoft Flow](https://flow.microsoft.com), edit the flow "Partner Referral to Microsoft Dynamics CRM Lead" that you imported in the section *[Import flow synchronization package](#import-flow-synchronization-package)*.</span></span>

    1. <span data-ttu-id="9cc52-193">Adja hozzá a Function alkalmazás URI azonosítóját a "web Hook-tanúsítvány érvényesítése" lépéshez.</span><span class="sxs-lookup"><span data-stu-id="9cc52-193">Add the value of the function app's URI to the "web hook certificate validation" step.</span></span>
    2. <span data-ttu-id="9cc52-194">Másolja és illessze be a Function alkalmazás visszahívási URI-JÁT a flow-dokumentumba.</span><span class="sxs-lookup"><span data-stu-id="9cc52-194">Copy and paste your function app's callback URI into the flow document.</span></span>
    3. <span data-ttu-id="9cc52-195">Mentse a folyamat dokumentumát.</span><span class="sxs-lookup"><span data-stu-id="9cc52-195">Save your flow document.</span></span>

#### <a name="sample-function-app-code"></a><span data-ttu-id="9cc52-196">Példa a Function alkalmazás kódjára</span><span class="sxs-lookup"><span data-stu-id="9cc52-196">Sample function app code</span></span>

```csharp
using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
using Microsoft.Azure.WebJobs;
using Microsoft.Extensions.Logging;
using System;
using System.IO;
using System.Linq;
using System.Net.Http;
using System.Security.Cryptography.X509Certificates;
using System.Text;
using System.Threading.Tasks;

public static async Task<IActionResult> Run(HttpRequest req, ILogger log)
{
    string requestBody = null;
    if (!string.IsNullOrWhiteSpace(GetFirstValueFromHeader(req, "x-ms-certificate-url")) && !string.IsNullOrWhiteSpace(GetFirstValueFromHeader(req, "x-ms-signature-algorithm")))
    {
        var certificateUrl = req?.Headers["x-ms-certificate-url"].First();
        try
        {
            string resultContent = null;
            using (var client = new HttpClient())
            {
                var result = await client.GetAsync(req.Headers["x-ms-certificate-url"].First());
                resultContent = await result.Content.ReadAsStringAsync();
                log.LogInformation(resultContent);
            }
            if (!string.IsNullOrEmpty(resultContent))
            {
                var certificate = new X509Certificate2(Encoding.UTF8.GetBytes(resultContent));
                var validationResult = certificate.Verify() && certificate.Issuer.Contains("O=Microsoft Corporation");
                if (validationResult)
                {
                    return new OkResult();
                }
                else
                {
                    return new BadRequestResult();
                }
            }
        }
        catch (Exception)
        {
            new BadRequestObjectResult("Certificate could not be retrieved, invalid caller to flow");
        }

        requestBody = await new StreamReader(req.Body).ReadToEndAsync();
        dynamic data = JsonConvert.DeserializeObject(requestBody);
    }
    else
    {
        new BadRequestObjectResult("Missing headers");
    }

    return new BadRequestObjectResult("Certificate validation failed");
}

private static string GetFirstValueFromHeader(HttpRequest request, string headerName)
{
    StringValues matchingHeaderValues;
    request.Headers.TryGetValue(headerName, out matchingHeaderValues);
    return matchingHeaderValues.Count != 0 ? matchingHeaderValues.First() : string.Empty;
}
```

### <a name="register-flow-with-partner-center"></a><span data-ttu-id="9cc52-197">Folyamat regisztrálása a partner Centerben</span><span class="sxs-lookup"><span data-stu-id="9cc52-197">Register flow with Partner Center</span></span>

<span data-ttu-id="9cc52-198">A flow-erőforrás regisztrálása a partner Centerben a folyamat elindításához és a webhook eseményeinek fogadásához:</span><span class="sxs-lookup"><span data-stu-id="9cc52-198">Register your flow resource with the Partner Center to trigger the flow and receive webhook events:</span></span>

1. <span data-ttu-id="9cc52-199">[Microsoft flow](https://flow.microsoft.com)a navigációs menüben válassza a **saját folyamatok** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="9cc52-199">In [Microsoft Flow](https://flow.microsoft.com), choose **My Flows** in the navigation menu.</span></span>
2. <span data-ttu-id="9cc52-200">Válassza ki a létrehozott vagy frissített folyamatot.</span><span class="sxs-lookup"><span data-stu-id="9cc52-200">Choose the flow you created or updated.</span></span>
3. <span data-ttu-id="9cc52-201">A folyamat lapon válassza a **folyamat szerkesztése** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="9cc52-201">On the flow page, choose **Edit flow**.</span></span>
4. <span data-ttu-id="9cc52-202">Másolja és mentse a folyamat **http post URL-címét**.</span><span class="sxs-lookup"><span data-stu-id="9cc52-202">Copy and save the flow's **HTTP POST URL**.</span></span> <span data-ttu-id="9cc52-203">Ezt az URL-címet kell használnia a folyamat elindításához.</span><span class="sxs-lookup"><span data-stu-id="9cc52-203">You will need to use this URL to trigger the flow.</span></span>
5. <span data-ttu-id="9cc52-204">[Regisztráljon a webhook-események fogadására,](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#register-to-receive-events) amikor a rendszer létrehozza vagy frissíti a hivatkozásokat.</span><span class="sxs-lookup"><span data-stu-id="9cc52-204">[Register to receive webhook events](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#register-to-receive-events) when referrals are created or updated.</span></span> <span data-ttu-id="9cc52-205">Használja a következő szövegtörzs-formátumot:</span><span class="sxs-lookup"><span data-stu-id="9cc52-205">Use the following body format:</span></span>

```json
{
    "WebhookUrl": "<<FlowUrl>>",
    "WebhookEvents": [
        "referral-created",
        "referral-updated"
    ],
    "signatureTokenToMsSignatureHeader": true
}
```
