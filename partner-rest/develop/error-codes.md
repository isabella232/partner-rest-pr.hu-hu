---
title: Partner API REST-hibakódok
description: A partner REST API-k egy JSON-objektumot adnak vissza a kérés sikeres vagy sikertelen állapotáról.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0829f48e5028b4a19e8a6f7b89fbb41d83a50cab
ms.sourcegitcommit: 0508b7302a3965fd5537b05c1f0397a1da014257
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/27/2020
ms.locfileid: "97770500"
---
# <a name="partner-api-rest-error-codes"></a>Partner API REST-hibakódok

A következőkre vonatkozik:

- Partner API

A partner REST API-kon lévő hibák a standard HTTP-állapotkódok, valamint egy JSON-hiba esetén is visszakerülnek.

## <a name="http-status-codes"></a>HTTP-állapotkódok

A következő táblázat felsorolja és leírja a visszaadott HTTP-állapotkódok listáját.

| Állapotkód | Állapotüzenet                  | Leírás                                                                                                                            |
|:------------|:--------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------|
| 400         | Hibás kérés                     | A kérelem nem dolgozható fel, mert helytelenül formázott vagy helytelen.                                                                       |
| 401         | Nem engedélyezett                    | A szükséges hitelesítő adatok hiányoznak vagy érvénytelenek az erőforráshoz.                                                   |
| 403         | Forbidden                       | A kért erőforráshoz való hozzáférés megtagadva. Lehet, hogy a felhasználó nem rendelkezik elegendő engedéllyel. **Fontos: Ha a feltételes hozzáférési szabályzatokat egy erőforrásra alkalmazza, előfordulhat, hogy a rendszer `HTTP 403; Forbidden error=insufficent_claims` visszaadja.** A Microsoft Graph és a feltételes hozzáférésről további részleteket a [Azure Active Directory feltételes hozzáférés fejlesztői útmutatója](https://docs.microsoft.com/azure/active-directory/develop/active-directory-conditional-access-developer) című témakörben talál.  |
| 404         | Nem található                       | A kért erőforrás nem létezik.                                                                                                  |
| 405         | A metódus nem engedélyezett              | A kérelemben szereplő HTTP-metódus nem engedélyezett az erőforráson.                                                                         |
| 406         | Nem elfogadható                  | Ez a szolgáltatás nem támogatja az Accept fejlécben kért formátumot.                                                                |
| 409         | Ütközés                        | Az aktuális állapot ütközik a kérés várt értékével. Előfordulhat például, hogy a megadott szülőmappa nem létezik.                   |
| 410         | Szűnt                            | A kért erőforrás már nem érhető el a kiszolgálón.                                               |
| 411         | Szükséges hossz                 | A kérelemhez Content-Length fejléc szükséges.                                                                                    |
| 412         | Sikertelen előfeltétel             | A kérelemben megadott előfeltétel (például egy if-Match fejléc) nem egyezik az erőforrás jelenlegi állapotával.                       |
| 413         | A kérelem entitása túl nagy        | A kérelem mérete meghaladja a maximális korlátot.                                                                                            |
| 415         | Nem támogatott adathordozó-típus          | A kérelem tartalmának típusa a szolgáltatás által nem támogatott formátum.                                                      |
| 416         | A kért tartomány nem teljesíthető | A megadott bájt-tartomány érvénytelen vagy nem érhető el.                                                                                    |
| 422         | Feldolgozható entitás            | A kérés nem dolgozható fel, mert szemantikailag helytelen.                                                                        |
| 423         | Zárolva                          | Az elérni kívánt erőforrás zárolva van.                                                                                          |
| 429         | Túl sok kérelem               | Az ügyfélalkalmazás szabályozása megtörtént, és nem próbálja meg megismételni a kérelmet, amíg az idő el nem telik.                |
| 500         | Belső kiszolgálóhiba           | Belső kiszolgálóhiba történt a kérelem feldolgozása közben.                                                                       |
| 501         | Nincs implementálva                 | A kért szolgáltatás nincs implementálva.                                                                                               |
| 503         | A szolgáltatás nem érhető el             | A szolgáltatás átmenetileg nem érhető el karbantartás céljából, vagy túlterhelt. A kérést késleltetés után megismételheti, amelynek a hossza Retry-After fejlécben adható meg.|
| 504         | Átjáró időtúllépése                 | A kiszolgáló, miközben proxyként működik, nem kapott időben választ a felsőbb rétegbeli kiszolgálótól, amelyhez a kérés teljesítésére tett kísérlet során szükség volt. Az 503-mel együtt fordulhat elő. |
| 507         | Nincs elegendő tárterület            | Elérte a maximális tárolási kvótát.                                                                                            |
| 509         | Túllépte a sávszélesség korlátját        | Az alkalmazás a maximális sávszélesség felső határának túllépése esetén lett szabályozva. Az alkalmazás többször is újrapróbálkozhat a kéréssel, miután a további idő eltelt. |

A hibaüzenet egyetlen JSON-objektum, amely egyetlen, **hiba** nevű tulajdonságot tartalmaz. Ez az objektum tartalmazza a hiba összes részletét. Az itt visszaadott információkat a HTTP-állapotkód mellett vagy a következő helyen is használhatja. A következő példa egy teljes JSON-hiba törzsét szemlélteti.

## <a name="error-resource-type"></a>Hiba erőforrástípus

A hibaüzenet egyetlen JSON-objektum, amely egyetlen, **hiba** nevű tulajdonságot tartalmaz. Ez az objektum tartalmazza a hiba összes részletét. Az itt visszaadott információkat a HTTP-állapotkód mellett vagy a következő helyen is használhatja. A következő példa egy teljes JSON-hiba törzsét szemlélteti.

A következő táblázat és kód minta egy adott hiba sémáját ismerteti.

| Név        | Típus   | Leírás                                                                                    |
|-------------|--------|------------------------------------------------------------------------------------------------|
| code        | sztring | Mindig vissza kell adni. Azt jelzi, hogy milyen típusú hiba történt. Nem null értékű.                          |
| message | sztring | Mindig vissza kell adni. Részletesen leírja a hibát, és további hibakeresési információkat biztosít. Nem null, nem üres. A maximális hossz 1024 karakter. |
| innerError        | object  | Választható. További hiba-objektum, amely a legfelső szintű hibánál konkrétabb lehet.                                   |
| cél      | sztring | Az a cél, ahol a hiba származik.                                                      |

### <a name="code-property"></a>Kód tulajdonság

A `code` tulajdonság a következő lehetséges értékek egyikét tartalmazza. Az alkalmazásoknak fel kell készülniük a hibák valamelyikének kezelésére.

| Code                      | Leírás
|:--------------------------|:--------------
| **accessDenied**          | A hívónak nincs engedélye a művelet végrehajtására.
| **generalException**      | Meghatározatlan hiba történt.
| **invalidRequest**        | A kérelem helytelen formátumú vagy helytelen.
| **itemNotFound**          | Az erőforrás nem található.
|**preconditionFailed**     | A kérelemben megadott előfeltétel (például egy if-Match fejléc) nem egyezik az erőforrás jelenlegi állapotával.
| **resourceModified**      | A frissítendő erőforrás módosult, mert a hívó utoljára elolvasta, általában egy eTag-eltérés.
| **serviceNotAvailable**   | A szolgáltatás nem érhető el. Próbálja megismételni a kérelmet egy késleltetés után. Retry-After fejléc lehet.
| **nem hitelesített**       | A hívó nincs hitelesítve.

### <a name="message-property"></a>Üzenet tulajdonsága

A `message` gyökérkönyvtárban található tulajdonság egy hibaüzenetet tartalmaz, amely a fejlesztőnek olvasásra szolgál. A hibaüzenetek nincsenek honosítva, és nem jelennek meg közvetlenül a felhasználó számára. Hibák kezelésekor a kód nem tudja ellenőrizni az `message` értékeket, mert bármikor megváltozhatnak, és gyakran tartalmaznak a sikertelen kérelemre vonatkozó dinamikus információkat. Csak a tulajdonságok között visszaadott hibakódokat kell megadnia `code` .

### <a name="innererror-object"></a>InnerError objektum

`innererror`Előfordulhat, hogy az objektum rekurzív módon több `innererror` objektumot tartalmaz, további, konkrétabb hibakódokkal. A hibák kezelésekor az alkalmazásoknak az összes rendelkezésre álló hibakódon át kell lenniük, és a legrészletesebb egyet kell használniuk.

Néhány további hiba is előfordulhat, hogy az alkalmazás a beágyazott `innererror` objektumokon belül találkozhat. Az alkalmazások nem szükségesek a kezeléséhez, de az is lehet, hogy ezek közül választhatnak. A szolgáltatás bármikor hozzáadhat új hibakódokat vagy visszaállíthatja a régieket, ezért fontos, hogy minden alkalmazás képes legyen kezelni az [alapszintű hibakódok]

```json
{
  "error": {
    "code": "unAuthorized",
    "message": "Caller is not authorized to access the resource.",
    "target": "referral",
    "innerError": {
      "code": "innerErrorCode",
      "message": "Unauthorized referral access"
    }
  }
}
```
