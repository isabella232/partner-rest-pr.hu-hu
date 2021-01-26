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
# <a name="referral-connectors"></a>Hivatkozó összekötők

Az átirányítási összekötők segítségével szinkronizálhatja a partneri hivatkozásokat az Ügyfélkapcsolat-kezelési (CRM) érdeklődőkkel. Az átirányítási összekötőt [Microsoft flow](https://flow.microsoft.com) használatával HTTPS-végpontként hozhatja létre a partneri átirányítások fogadásához. Ezután megírhatja a folyamat által a CRM rendszernek érdeklődőként kapott átirányítást.

## <a name="prerequisites"></a>Előfeltételek

* Előfizetés Microsoft Flow
  * Fiók rendszergazdai hozzáféréssel ehhez az előfizetéshez
* Azure Active Directory (Azure AD) alkalmazás-azonosító, felhasználói azonosító, jelszó és bérlő azonosítója (a partner API eléréséhez használatos). A telepítési utasításokért lásd: [partner-hitelesítés](api-authentication.md).
* [Azure Function app](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) -előfizetés.
* A [partneri központ webhook esemény](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events) -előfizetése a [létrehozott](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-created-event) és a [hivatkozó frissített](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-updated-event) eseményekre.
* [Microsoft Dynamics 365](https://dynamics.microsoft.com) -előfizetés
  * Értékesítési modul engedélyezve
  * Fiók rendszergazdai hozzáféréssel ehhez az előfizetéshez

## <a name="flow-overview"></a>A flow áttekintése

Az átirányítások importálása a CRM-be a következő folyamat használatával történik:

1. A partner egy webhookot állít be az átirányítási értesítések fogadásához.
2. A partner regisztrálja a webhookot a partner centerrel. A partner arra is előfizet, hogy mikor hozza létre vagy frissíti a webhook eseményeit.
3. Az Ajánlói ügyfél létrehoz vagy frissít egy átirányítást.
4. A partner Center webhook rendszer ellenőrzi a partner regisztrációját, és értesítést küld a webhooknak.
5. A webhook megkapja az értesítést.
6. A Microsoft flow-ban található flow-dokumentum tokent használ a partner Center Referral API meghívásához.
7. A flow-végpont megkapja az átirányítást.
8. A flow-végpont létrehozza a CRM-érdeklődőt.

![Az ebben a szakaszban ismertetett lépéseket a partnerek CRM-be történő importálásának folyamata című szakasz mutatja.](../images/referralwebhook.png)

## <a name="flow-document-process"></a>Flow-dokumentum folyamata

Az átirányítási összekötőhöz tartozó flow-dokumentum a Dynamics 365-ből származó CRM-érdeklődővel szinkronizál egy partneri hivatkozást.

1. Az összekötő lekérdezi a csatlakozáshoz szükséges tokent `https://api.partner.microsoft.com/v1.0/engagements/referrals` .
2. Az összekötő beolvassa az összekötőt a használatával indító hivatkozással `https://api.partner.microsoft.com/v1.0/engagements/referrals/{id}` .
3. Az összekötő a Dynamics 365-hoz csatlakozik.
4. Az összekötő létrehoz egy új érdeklődőt, vagy frissít egy meglévő érdeklődőt az átirányítással kapcsolatos legfrissebb információkkal.
5. Az összekötő frissítései a CRM-érdeklődő legújabb frissítéseire hivatkoznak.

![Az ebben a szakaszban szereplő lépéseket bemutató folyamatábra.](../images/ReferralFlowSteps.png)

## <a name="sample-referral-connector"></a>Példa Ajánlói összekötő

A következő *minta-átirányítási összekötő* bemutatja, hogyan szinkronizálhat a partner Center-hivatkozásokat a CRM-érdeklődők számára a Dynamics 365-ben.

> [!IMPORTANT]
> Más CRM is írhat, ha a minta kódjában lecseréli a [flow-összekötőket](https://flow.microsoft.com/en-us/connectors/) .

### <a name="import-flow-synchronization-package"></a>Adatfolyam-szinkronizálási csomag importálása

Töltse le és importálja a *mintakód-csomagot* a Microsoft Flowba, és kapcsolódjon a Dynamics 365-hez:

1. Töltse le a [flow szinkronizációs csomagot](https://github.com/microsoft/Partner-Center-Referrals/blob/master/flowconnectors/MicrosoftDynamicsCRM/PartnerReferralsToDynamicsCRMLead.zip?raw=true) a [GitHub](https://github.com/microsoft/Partner-Center-Referrals)-adattárból.
2. A megfelelő hitelesítő adatok használatával jelentkezzen be [Microsoft flow](https://flow.microsoft.com) .
3. Válassza a **saját folyamatok** lehetőséget a navigációs menüben. Ezután válassza az **Importálás** lehetőséget.
4. A **csomag importálása** lapon válassza ki a letöltött flow szinkronizációs csomagot. Ezután válassza a **feltöltés** lehetőséget.

    ![Csomag importálása képernyő](../images/importPackage.png)

5. A csomag feltöltésének befejezése után keresse meg a csomag **tartalmának áttekintése** lapon feltöltött csomagot.

    ![A csomag importálása képernyő részletei](../images/importPackageDetails.png)

6. Válassza a **művelet** gombot (ceruza ikon) a feltöltött csomaghoz. Ekkor megnyílik a **telepítő importálása** panel.
7. Válassza ki a **telepítési** típust.

    * Új folyamat létrehozásához válassza a **Létrehozás új néven** lehetőséget, majd adjon meg egy új **nevet**.
    * Ha egy meglévő folyamatot ugyanazzal a névvel szeretne frissíteni, válassza a **frissítés** lehetőséget.

    ![Új csomagjának felvétele-képernyő létrehozása vagy frissítése](../images/CreateNewConnection.png)

8. A **csomag importálása** oldalon keresse meg a Dynamics 365-kapcsolatát a **kapcsolódó erőforrások** szakasz **Tartalom áttekintése** szakaszában.
9. Válassza a **művelet** gombot (ceruza ikon) a Dynamics 365-kapcsolathoz. Ekkor megnyílik a kapcsolódó erőforrás **Importálás beállítása** panelje.
10. Válassza az **új létrehozása** elemet, és hozzon létre egy új Dynamics 365-kapcsolatokat, vagy válasszon ki egy meglévőt.
11. Győződjön meg arról, hogy a **csomag importálása** lap most megjeleníti a kiválasztott flow-telepítési típust és a Dynamics 365-kapcsolatokat. Ezután válassza az **Importálás** lehetőséget.

    ![Csomag állapotának importálása képernyő](../images/importStatus.png)

12. Győződjön meg arról, hogy a flow-erőforrás létrehozása vagy frissítése megtörtént.

### <a name="configure-flow-parameters"></a>Folyamat paramétereinek konfigurálása

Adja meg a flow-erőforrás paramétereit:

1. [Microsoft flow](https://flow.microsoft.com)a navigációs menüben válassza a **saját folyamatok** lehetőséget.
2. Válassza ki az előző szakaszban létrehozott vagy frissített folyamat-erőforrást.
3. A folyamat lapon válassza a **folyamat szerkesztése** lehetőséget.
4. Válassza ki az **HRE-(ügyfél-) azonosító** változót, és adja meg az Azure ad-alkalmazás azonosítóját.
5. Válassza ki a **userid** változót, és adja meg a felhasználói azonosítóját.
6. Válassza ki a **userPassword** változót, és adja meg a felhasználói jelszavát.
7. Válassza ki a **HRE-Directory (bérlő) azonosító** változót. Adja meg az Azure AD-alkalmazás bérlői AZONOSÍTÓját.
8. Válassza a **Mentés** lehetőséget a folyamat mentéséhez.

    ![Flow változók beállításai képernyő](../images/SetFlowVariables.png)

### <a name="authenticate-the-callback"></a>A visszahívás hitelesítése

Hitelesítse a visszahívási eseményt a partner központjától:

> [!TIP]
> Példaként tekintse meg a [minta Function alkalmazás kódját](#sample-function-app-code) a következő szakaszban.

1. [Hozzon létre egy Azure Function-alkalmazást](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) , amely [hitelesíti a visszahívási eseményt a partner Centertől](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#how-to-authenticate-the-callback).

    1. Győződjön meg arról, hogy a szükséges fejlécek jelen vannak (**Authorization**, **x-MS-Certificate-URL** és **x-MS-Signature-algoritmus**).
    2. Töltse le a tartalom aláírásához használt tanúsítványt (**x-MS-Certificate-URL**).
    3. Ellenőrizze a tanúsítványlánc utasításait.
    4. Ellenőrizze a tanúsítvány **szervezetét** .
    5. Az UTF-8 kódolású tartalom beolvasása pufferbe.
    6. Hozzon létre egy RSA titkosítási szolgáltatót.
    7. [Ellenőrizze, hogy az aláírás egyezik-e](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#example-for-signature-validation) a megadott kivonatoló algoritmussal (például sha256).
    8. Ha az ellenőrzés sikeres, a rendszer egy **OK** üzenetet ad vissza.

2. Figyelje meg a Function app HTTP-végpontjának generált visszahívási URI azonosítóját. Ez az URI a Function alkalmazás létrehozásakor jelenik meg. Ezt az URI-t a Function alkalmazás Azure Resource lapján is megtalálhatja.
3. A [Microsoft Flowban](https://flow.microsoft.com)szerkessze a "partneri javaslat a Microsoft Dynamics CRM-vezetőhöz" című szakaszt, amelyet az *[importálási folyamat szinkronizációs csomagja](#import-flow-synchronization-package)* című szakaszban importált.

    1. Adja hozzá a Function alkalmazás URI azonosítóját a "web Hook-tanúsítvány érvényesítése" lépéshez.
    2. Másolja és illessze be a Function alkalmazás visszahívási URI-JÁT a flow-dokumentumba.
    3. Mentse a folyamat dokumentumát.

#### <a name="sample-function-app-code"></a>Példa a Function alkalmazás kódjára

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

### <a name="register-flow-with-partner-center"></a>Folyamat regisztrálása a partner Centerben

A flow-erőforrás regisztrálása a partner Centerben a folyamat elindításához és a webhook eseményeinek fogadásához:

1. [Microsoft flow](https://flow.microsoft.com)a navigációs menüben válassza a **saját folyamatok** lehetőséget.
2. Válassza ki a létrehozott vagy frissített folyamatot.
3. A folyamat lapon válassza a **folyamat szerkesztése** lehetőséget.
4. Másolja és mentse a folyamat **http post URL-címét**. Ezt az URL-címet kell használnia a folyamat elindításához.
5. [Regisztráljon a webhook-események fogadására,](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#register-to-receive-events) amikor a rendszer létrehozza vagy frissíti a hivatkozásokat. Használja a következő szövegtörzs-formátumot:

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
