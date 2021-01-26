---
title: Partner API REST-fejlécek
description: A partner REST API a következő HTTP-kérést és válasz-fejléceket támogatja.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 955cab07da7f3a386690e18042165015906d864a
ms.sourcegitcommit: 0508b7302a3965fd5537b05c1f0397a1da014257
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/27/2020
ms.locfileid: "97770401"
---
# <a name="partner-rest-api-headers"></a>Partner REST API fejlécek

A partner REST API a következő HTTP-kérelem és-válasz fejléceket támogatja.

> [!NOTE]
> Nem minden API-hívás fogadja el az összes fejlécet.

## <a name="request-headers"></a>Kérésfejlécek

A partner REST API a következő HTTP-kérések fejléceit támogatja.

| Fejléc                       | Érték típusa | Leírás                                                                            |
|------------------------------|------------|----------------------------------------------------------------------------------------|
| Engedélyezés           | sztring     | Kötelező. Az engedélyezési jogkivonat az űrlap tulajdonosi &lt; jogkivonatában &gt; .                    |
| Elfogadás                  | sztring     | Megadja a kérelem és a válasz típusát: "Application/JSON".                           |
| ügyfél-kérelem azonosítója         | GUID       | Kötelező. A hívás egyedi azonosítója, hasznos a naplókhoz és a hálózati nyomkövetésekhez a hibák elhárítása érdekében. Az értéket minden hívásnál alaphelyzetbe kell állítani. Az összes műveletnek tartalmaznia kell ezt a fejlécet. |
| If-Match:                    | sztring     | A Egyidejűség-vezérléshez használatos. Néhány API-híváshoz a If-Match fejlécen keresztül kell átadni a ETag. A ETag általában az erőforráson van, ezért a legújabbat kell megszereznie. |

## <a name="response-headers"></a>Válaszfejlécek

A partner REST API a következő HTTP-válasz fejléceket is visszaadja.

| Fejléc                    | Érték típusa | Leírás                                                                                                               |
|-------------------|------------|--------------------------------------------------------------------------------------------------|
| Elfogadás                | sztring     | Megadja a kérelem és a válasz típusát: "Application/JSON".                                     |
| kérelem azonosítója        | GUID       | A hívás egyedi azonosítója, amely az azonosító-hatékonyság biztosítására szolgál. Időtúllépés esetén az újrapróbálkozási hívásnak ugyanazt az értéket kell tartalmaznia. A válasz fogadása (sikeres vagy üzleti hiba) esetén az értéket vissza kell állítani a következő híváshoz. |
| ügyfél-kérelem azonosítója| GUID| A hívás egyedi azonosítója, hasznos a naplók és a hálózati nyomkövetés a hibák elhárításához. Az értéket minden hívásnál alaphelyzetbe kell állítani. Az összes műveletnek tartalmaznia kell ezt a fejlécet.                                                |
| x-MS-AGS-diagnosztika   | sztring | Egy karakterlánc, amely a szolgáltatásból származó diagnosztikai adatokat tartalmaz.
| időbélyeg|sztring | A kérés időbélyege, amikor eléri az API-t.
|ETag |sztring | Az erőforrás ETag.
