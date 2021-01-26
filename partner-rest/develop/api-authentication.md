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
# <a name="partner-api-authentication"></a>Partner API hitelesítése

A következőkre vonatkozik:

- Partner API

A partner API a Azure Active Directoryt (Azure AD) használja a hitelesítéshez. Ha együttműködik a partner API-val, megfelelően konfigurálnia kell egy Azure AD-alkalmazást, és be kell szereznie egy hozzáférési jogkivonatot. Hozzáférési jogkivonatokat kérhet az [alkalmazás-és felhasználói hozzáféréshez](#application-and-user-access) , vagy [csak az alkalmazáshoz való hozzáférést](#application-only-access).

## <a name="application-and-user-access"></a>Alkalmazás-és felhasználói hozzáférés

Ez a módszer ajánlott az **alkalmazás-és felhasználói hozzáférés** beállításához az API-hoz.

1. Jelentkezzen be az [Azure Portalra](https://portal.azure.com/).
2. Válassza ki a **Azure Active Directory** szolgáltatást.
3. Válassza a **Alkalmazásregisztrációk**, majd az **új alkalmazás regisztrálása** lehetőséget.
4. Hozza létre az új alkalmazást. Az **alkalmazás típusa** mezőben válassza a **natív** lehetőséget. Adjon meg egy nevet és egy URL-címet, majd válassza a **Létrehozás** lehetőséget.
5. Válassza ki az alkalmazás **API-engedélyeit** . Az **API-engedélyek kérése** képernyőn válassza az **engedély hozzáadása**, majd a **szervezet által használt API** -k elemet.
6. Keressen rá a *Microsoft partner* (*Microsoft dev Center*) API ( `4990cffe-04e8-4e8b-808a-1175604b879f` ) kifejezésre.

    ![Képernyőkép a kérelem API-engedélyeiről képernyőről a Microsoft partner API-val való kereséssel](../images/SearchGatewayApi.png)

7. Állítsa be a **delegált engedélyeket** a **partner központba**.

    ![Képernyőkép a delegált engedélyek konfigurációs képernyőjéről a Microsoft partner API-hoz](../images/SelectUserPermission.png)
    
8. Keressen rá a *Microsoft partner* (*Microsoft partner Center*) API ( `fa3d9a0c-3fb0-42cc-9193-47c7ecd2edbd` ) kifejezésre.

    ![Képernyőkép a kérelmek API-engedélyeiről képernyőről a Microsoft partner Center API-val való kereséssel](../images/SearchPCApi.png)
    
9. Válassza ki a **Microsoft partner centert** , és jelölje be a **user_impersonation**.

10. Állítsa be a **delegált engedélyeket** a **partner központba**.

    ![Képernyőkép a delegált engedélyek konfigurációs képernyőjéről a Microsoft partner Center API-hoz](../images/SelectPCUserPermission.png)

## <a name="application-only-access"></a>Csak alkalmazáshoz való hozzáférés

Ez a metódus csak az API **-khoz való alkalmazás-hozzáférés** beállításához ajánlott.

> [!IMPORTANT]
> Meg kell adnia az alkalmazás AZONOSÍTÓját, az alkalmazás kulcsát és a címtár AZONOSÍTÓját az Azure AD-alkalmazásból.

1. Jelentkezzen be az [Azure Portalra](https://portal.azure.com/).
2. Válassza ki a **Azure Active Directory** szolgáltatást.
3. Válassza a **Alkalmazásregisztrációk** lehetőséget, majd válassza az **új alkalmazás regisztrálása** lehetőséget.
4. Hozza létre az új alkalmazást. Az **alkalmazás típusa mezőben** válassza a **Web App/API** lehetőséget. Adja meg az alkalmazás **nevét** és **URL-címét**. Ezután válassza a **Létrehozás** elemet.
5. Válassza ki az alkalmazás **API-engedélyeit** . Válassza az **engedély hozzáadása** lehetőséget, majd **a saját szervezet által használt API** -k elemet.
6. Keressen rá a *Microsoft partner* (*Microsoft dev Center*) API ( `4990cffe-04e8-4e8b-808a-1175604b879f` ) kifejezésre.

    ![Képernyőkép a kérelem API-engedélyeiről képernyőről a Microsoft partner API-val való kereséssel](../images/SearchGatewayApi.png)

7. Állítsa be a **delegált engedélyeket** a **partner központba**.

    ![Képernyőkép a delegált engedélyek konfigurációs képernyőjéről a Microsoft partner API-hoz](../images/SelectUserPermission.png)

8. A regisztrált alkalmazáshoz válassza a **Tulajdonságok** lehetőséget, majd válassza **az alkalmazás azonosítójának másolása** lehetőséget.
9. Válassza a **Beállítások**, majd a **tanúsítványok & Secrets** elemet. Válassza az **új ügyfél titkot** , és állítsa a **lejárat**  lehetőséget, hogy **Soha ne járjon le**. Ezután válassza a **Mentés** lehetőséget.
10. A **kulcsok** menüben válassza **a kulcs értékének másolása** lehetőséget. Mentse az érték másolatát.

> [!WARNING]
> Ne felejtse el menteni a kulcs értékének másolatát a létrehozott kulcshoz. Ezt a kulcs értéket később kell használnia a jogkivonat beszerzéséhez.

## <a name="partner-consent"></a>Partneri beleegyezett

Az Azure felügyeleti portálján válassza a **vállalati alkalmazások** lehetőséget. Keresse meg az előző szakaszban létrehozott alkalmazást, és válassza ki az alkalmazást. Válassza az **engedélyek** lehetőséget, majd válassza **a rendszergazdai jóváhagyás megadása partner fiókhoz** lehetőséget.
