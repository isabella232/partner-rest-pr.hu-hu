---
title: Javaslati erőforrások
description: Az átirányítási erőforrások egy, az ügyféltől, a Microsofttól vagy egy másik partnertől származó közvetlen értékesítési vezetőt jelölnek.
ms.date: 05/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 08438d208da57a4df40aeb609b14b6b6a6128d45
ms.sourcegitcommit: 0508b7302a3965fd5537b05c1f0397a1da014257
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/27/2020
ms.locfileid: "97770397"
---
# <a name="referral-resources"></a>Javaslati erőforrások

A következőkre vonatkozik:

- Partnerközpont

Ezek az erőforrások közvetlen értékesítést jelentenek az ügyféltől, a Microsofttól vagy egy másik partnertől.

## <a name="referral"></a>Hivatkozási

Az átirányítást jelöli.

| Tulajdonság              | Típus                                              | Leírás                                                                                                       |
|-----------------------|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| Id                    | sztring                                            | Az átirányításhoz tartozó azonosító.                                                                                         |
| EngagementId          | sztring                                            | Az ajánló EngagementID. Több hivatkozás is társítható egyetlen EngagementID                 |
| Name                  | sztring                                            | Az ajánló neve.                 |
| ExternalReferenceId   | sztring                                            | Az átirányításhoz tartozó külső azonosító. Példa: saját Dynamics 365 érdeklődő/lehetőség AZONOSÍTÓjának tárolása                    |
| CreatedDateTime       | karakterlánc UTC-dátum időformátuma                    | Az átirányítás létrehozásának dátuma.                                                                                |
| UpdatedDateTime       | karakterlánc UTC-dátum időformátuma                    | Az átirányítás utolsó frissítésének dátuma.                                                                           |
| ExpirationDateTime    | karakterlánc UTC-dátum időformátuma                    | Az átirányítás érvényességének dátuma.                                                                                |
| Állapot                | [ReferralStatus](referral-resources.md#referralstatus)      | Egy [enumerálás](https://docs.microsoft.com/dotnet/api/system.enum) az átirányítási állapotot jelző értékekkel. |
| Részállapot          | [ReferralSubstatus](referral-resources.md#referralsubstatus)      | Az átirányítási alállapotot jelző értékekkel rendelkező [enumerálás](https://docs.microsoft.com/dotnet/api/system.enum) . |
| StatusReason          | sztring                                            | Az állapottal kapcsolatos leíró üzenet. Példa: Miért elveszett az átirányítás? |
| ReferralType          | [ReferralType](referral-resources.md#referraltype)          | Az átirányítási típust jelöli.                                                                                     |
| Minősítés         | [ReferralQualification](referral-resources.md#referralqualification)| Az ajánló minőségét jelöli.                                                                           |
| CustomerProfile       | [CustomerProfile](referral-resources.md#customerprofile)    | Információ az ügyfélről.                                                                                     |
| Hozzájárulás               | [Hozzájárulás](referral-resources.md#consent)                    | A hozzájárulási jelzők az információk megosztását más szervezetekkel, és lehetővé teszik a felhasználóknak való kapcsolatfelvételt.         |
| Részletek               | [ReferralDetails](referral-resources.md#referraldetails)    | Vásárlói adatok, megjegyzések, ügyleti érték, pénznem zárási dátuma.                                                                |
| Csoport                  | [Tag](referral-resources.md#member)                      | A résztvevő szervezetekben lévő felhasználókat jelöli.                                |
| InviteContext         | [InviteContext](referral-resources.md#invitecontext)        | A felhasználó által megadható további információkat jelenít meg egy másik szervezetnek a partneri szerepvállaláshoz való meghívásakor.  |
| ETag                  | sztring                                            | Az erőforrások frissítésekor a Etagek használata és a Egyidejűség-ellenőrzés szükséges. |
| Cél         | [ReferralTarget](referral-resources.md#target)        | A felhasználó által megadható további információkat jelenít meg egy másik szervezetnek a partneri szerepvállaláshoz való meghívásakor.  |

## <a name="referralstatus"></a>ReferralStatus

Egy [enumerálás](https://docs.microsoft.com/dotnet/api/system.enum) az átirányítási állapotot jelző értékekkel.

| Érték           | Leírás                                                                                |
|-----------------|---------------------------------------------------------------------------------------------|
| Nincs            |                                                                                             |
| Új             | Új hivatkozót jelöl.                                                                 |
| Aktív          | Aktív hivatkozót jelöl.                                                             |
| Lezárt          | Lezárt hivatkozót jelöl.                                                              |

## <a name="referralsubstatus"></a>ReferralSubstatus

Egy [enumerálás](https://docs.microsoft.com/dotnet/api/system.enum) az átirányítási állapotot jelző értékekkel.

| Érték           | Leírás                                                                                |
|-----------------|--------------------------------------------------------------------------------------------|
| Nincs            |                                                                                            |
| Függőben         | Egy függőben lévő új hivatkozót jelöl.                                                 |
| Megérkezett        | A kapott új hivatkozót jelöli.                   |
| Elfogadva        | Egy elfogadott aktív hivatkozót jelöl.                                                    |
| Megnyert             | A megnyert lezárt átirányítást jelöli.                                            |
| Elveszett            | Egy lezárt átirányítást jelöl, amely elveszett.                                           |
| Elutasítva        | Egy lezárt átirányítást jelöl, amelyet a rendszer visszautasított.                                       |
| Lejárt         | Egy lejárt lezárt átirányítást jelöl.                                             |

### <a name="status--substatus-transition-states"></a>Állapot & állapot átmeneti állapotai

| Állapot                | Engedélyezett állapot-váltás     | Engedélyezett alállapot                |
|-----------------------|-------------------------------|---------------------------------------|
| Új                   | Új, aktív, lezárt           | Függőben, fogadva                     |
| Aktív                | Aktív, lezárt                | Elfogadva                              |
| Lezárt                | Lezárt                        | Megnyert, elveszett, visszautasított, lejárt          |

## <a name="referraltype"></a>ReferralType

Az átirányítási típust jelző értékeket tartalmazó [enumerálás](https://docs.microsoft.com/dotnet/api/system.enum) .

| Tulajdonság              | Leírás                                                                     |
|-----------------------|---------------------------------------------------------------------------------|
| Megosztott                | Egy olyan hivatkozást jelöl, amelyben az összes érintett fél együtt fog működni a bezárással.  |
| Független           | Egy olyan hivatkozást jelöl, amelyben két fél fog működni a bezáráshoz.           |

## <a name="referralqualification"></a>ReferralQualification

Egy [enumerálás](https://docs.microsoft.com/dotnet/api/system.enum) az átirányítási állapotot jelző értékekkel.

| Érték                | Leírás                                                                                 |
|----------------------|---------------------------------------------------------------------------------------------|
| Nincs                 | Olyan hivatkozást jelöl, amelyhez nincs hozzárendelve minőségi mérték.                               |
| Direct               | Egy közvetlenül az ügyfél által létrehozott hivatkozást jelöl.                         |
| MarketingQualified   | A Microsoft Marketing Automation Systems használatával generált átirányítást jelöl.   |
| SalesQualified       | Egy Microsoft értékesítési ügynökre mutató hivatkozást jelöl.                                         |

## <a name="customerprofile"></a>CustomerProfile

Az ügyfél kapcsolattartási adatait tartalmazza.

| Tulajdonság | Típus                                                   | Leírás                                            |
|----------|--------------------------------------------------------|--------------------------------------------------------|
| Név     | sztring                                                 | Az ügyfél szervezetének neve.                        |
| Cím  | [Cím](referral-resources.md#address)                         | Az ügyfél címe.                           |
| Méret     | sztring                                                 | Az ügyfelek szervezeténél dolgozó alkalmazottak száma. |
| Csoport     | [Tag](referral-resources.md#member)                           | Az ügyfél szervezetéhez tartozó névjegyek.            |
| Azonosítók      | [CustomerProfileType](referral-resources.md#customerprofiletype) | Az ügyfél külső azonosítóit jelző értékek [tömbje](https://docs.microsoft.com/dotnet/api/system.array) .                        |

## <a name="customerprofiletype"></a>CustomerProfileType

Az ügyfél külső azonosítóit tartalmazza.

| Tulajdonság | Típus   | Leírás                                                                           |
|----------|--------|---------------------------------------------------------------------------------------|
| Duns     | sztring | Az ügyfél [Dun & bradstreettől száma](https://www.dnb.com/duns-number.html) . |
| Külső | sztring | A szervezete számára egyedi ügyfél-azonosító.                                            |

## <a name="address"></a>Cím

Az ügyfélhez használni kívánt e-mail.

| Tulajdonság     | Típus   | Leírás                                                |
|--------------|--------|------------------------------------------------------------|
| AddressLine1 | sztring | A címe első sora.                             |
| AddressLine2 | sztring | A címe második sora. Ez a tulajdonság nem kötelező. |
| City         | sztring | A város.                                                  |
| Állam        | sztring | Az állapot.                                                 |
| Irányítószám   | sztring | A zip-kód vagy postai irányítószám                                |
| Ország      | sztring | Az ország/régió [ISO-országkód szerinti formátuma](https://docs.microsoft.com/dotnet/api/system.globalization.regioninfo.threeletterisoregionname?view=netframework-4.7.2).             |
| Region       | sztring | A régió.                                                |

## <a name="member"></a>Tag

Egy adott személy kapcsolattartási adatait ismerteti.

| Tulajdonság    | Típus   | Leírás                  |
|-------------|--------|------------------------------|
| FirstName   | sztring | A partner vezetékneve.    |
| LastName    | sztring | A partner vezetékneve.     |
| PhoneNumber | sztring | A partner telefonszáma.  |
| E-mail       | sztring | A partner e-mail-címe. |
| ContactPreference       | [ContactPreference](referral-resources.md#contactpreference) | A partner e-mail-értesítések fogadására vonatkozó beállításai. |

## <a name="contactpreference"></a>ContactPreference

Az e-mail-értesítések fogadásának kapcsolattartási beállításait ismerteti.

| Tulajdonság    | Típus   | Leírás                  |
|-------------|--------|------------------------------|
| Területi beállítás   | sztring | Az e-mail-értesítés területi beállítása. A [AllCultures](https://docs.microsoft.com/dotnet/api/system.globalization.culturetypes?view=netframework-4.7.2#System_Globalization_CultureTypes_AllCultures), a [NeutralCultures](https://docs.microsoft.com/dotnet/api/system.globalization.culturetypes?view=netframework-4.7.2#System_Globalization_CultureTypes_NeutralCultures)és a [SpecificCultures](https://docs.microsoft.com/dotnet/api/system.globalization.culturetypes?view=netframework-4.7.2#System_Globalization_CultureTypes_SpecificCultures) támogatottak  |
| DisableNotifications    | logikai | Letiltja az e-mailes értesítéseket a felhasználó számára.     |

## <a name="consent"></a>Hozzájárulás

A hozzájárulási jelzők az információk megosztását más szervezetekkel, és lehetővé teszik a felhasználóknak való kapcsolatfelvételt.

| Tulajdonság                                         | Típus      | Leírás                                                                                |
|--------------------------------------------------|-----------|--------------------------------------------------------------------------------------------|
| ConsentToToShareInfoWithOthers                   | boolean   | Azt jelzi, hogy a személyazonosításra alkalmas adatok másokkal való megosztásának beleegyezik.             |
| ConsentToContact                                 | boolean   | Azt jelzi, hogy a felhasználók kapcsolatba léphetnek.  |

## <a name="invitecontext"></a>InviteContext

További információ, amely megosztható egy másik szervezet meghívásakor.

| Tulajdonság              | Típus                                                       | Leírás                                                                   |
|-----------------------|------------------------------------------------------------|-------------------------------------------------------------------------------|
| Jegyzetek                 | sztring                                                     | További megjegyzések a fogadó szervezethez.                |
| InvitedBy | [InvitedBy](referral-resources.md#invitedby)                                     | Az átirányítást küldő szervezeti azonosító.                                   |

## <a name="invitedby"></a>InvitedBy

További információ, amely megosztható egy másik szervezet meghívásakor.

| Tulajdonság              | Típus                                                       | Leírás                                                                   |
|-----------------------|------------------------------------------------------------|-------------------------------------------------------------------------------|
| OrganizationId (Szervezeti azonosító)        | sztring                                                     | Az átirányítást küldő szervezeti azonosító.                |
| OrganizationName      | sztring                                                     | Az átirányítást küldő szervezet neve.                                   |

## <a name="referraldetails"></a>ReferralDetails

Az átirányítási adatokat jelöli.

| Tulajdonság              | Típus                                                       | Leírás                                                                   |
|-----------------------|------------------------------------------------------------|-------------------------------------------------------------------------------|
| Jegyzetek                 | sztring                                                     | További megjegyzések a fogadó szervezethez.                |
| DealValue             | decimal                                                    | Az átirányítás értéke.                                    |
| Pénznem              | sztring                                                    | Az [ISO 4217 pénznemének szimbóluma](https://docs.microsoft.com/dotnet/api/system.globalization.regioninfo.isocurrencysymbol?view=netframework-4.7.2)                                   |
| ClosingDateTime       | karakterlánc UTC-dátum időformátuma                         | Az a dátum, ameddig az ügyfélnek a bezárását szeretné.                           |
| Követelmények          | [ReferralRequirements](referral-resources.md#referralrequirements)   | Az iparág, a termékek, a szolgáltatástípus és a megoldások, amelyekre az ügyfél érdeklődik.|

## <a name="referralrequirements"></a>ReferralRequirements

Az ügyfélre vonatkozó követelményeket tartalmazza.

| Tulajdonság        | Típus                                                         | Leírás                                          |
|-----------------|--------------------------------------------------------------|------------------------------------------------------|
| Iparágak      | [Tag](referral-resources.md#tag)                                       | Az az iparág, amelyre az ügyfél érdeklődik.        |
| Termékek        | [Tag](referral-resources.md#tag)                                       | Az ügyfél által érintett termékek.          |
| Szolgáltatások        | [Tag](referral-resources.md#tag)                                       | Az ügyfél által érintett szolgáltatások.          |
| Megoldások       | [SolutionTag](referral-resources.md#solutiontag)                       | Az ügyfél által érintett megoldások.                             |

## <a name="solutiontag"></a>SolutionTag

A megoldás részleteit tartalmazza.

| Tulajdonság        | Típus                                         | Leírás                                          |
|-----------------|----------------------------------------------|------------------------------------------------------|
| Id              | sztring                                       | A megoldás azonosítója.        |
| Name            | sztring                                       | A megoldás neve.          |
| Megoldástípusa    | [Megoldástípusa](referral-resources.md#solutiontype)     | A megoldás típusa.          |

## <a name="solutiontype"></a>Megoldástípusa

Egy [enumerálás](https://docs.microsoft.com/dotnet/api/system.enum) a megoldás típusát jelző értékekkel.

| Tulajdonság        | Leírás                                                     |
|-----------------|-----------------------------------------------------------------|
| Nincs            |                                                                  |
| Kategória        |  Kihasználja az előre definiált megoldások nevét.                            |
| Name            |  A Microsoft Catalog megoldásait is hivatkozhatjuk. |

## <a name="target"></a>Cél

Az átirányítási cél leírása.

| Tulajdonság                  | Típus                                                  | Leírás                                                   |
|---------------------------|-------------------------------------------------------|---------------------------------------------------------------|
| Id                        | sztring                                                | Az átirányítási cél azonosítója. |
| Típus                      | [ReferralTargetType](referral-resources.md#targettype) | Hivatkozó cél típusa |

## <a name="targettype"></a>TargetType

Egy [enumerálás](https://docs.microsoft.com/dotnet/api/system.enum) a megoldás típusát jelző értékekkel.

| Tulajdonság        | Leírás                                                     |
|-----------------|-----------------------------------------------------------------|
| Nincs            |                                                                  |
| BusinessProfileLocation         |  Profil helye a partner üzleti profiljában.                            |
| SolutionProfile            |  A partner Solution profilja. |

## <a name="tag"></a>Címke

Leírja a címkét.

| Tulajdonság                  | Típus                                                  | Leírás                                                   |
|---------------------------|-------------------------------------------------------|---------------------------------------------------------------|
| Id                        | sztring                                                | A címke azonosítója.                                          |

### <a name="products"></a>Termékek

| Érték        |
|-----------------|
|Azure|
|EnterpriseMobilityAndSecurity|
|Exchange|
|DeveloperTools|
|Dynamics365Business|
|Dynamics365Enterprise|
|DynamicsAX, GP, NAV, SL|
|Microsoft365|
|Office|
|PowerBI|
|Project|
|SharePoint|
|SkypeForBusiness|
|Surface|
|SurfaceHub|
|SQL|
|Teams|
|Visio|
|Windows|
|Yammer|

### <a name="services"></a>Szolgáltatások

| Érték        |
|-----------------|
|ConsultingAndProfessional|
|CustomSolution (ISV)|
|DeploymentOrMigration|
|Hardver|
|Integráció|
|IPServices (ISV)|
|LearningAndCertification|
|Licencek|
|ManagedServices|
|ProjectServices|

### <a name="industries"></a>Iparágak

| Érték        |
|-----------------|
|Mezőgazdaság, erdészet, & horgászat|
|Kommunikáció & média|
|Education|
|Pénzügyi szolgáltatások|
|Államigazgatás|
|Egészségügy|
|Vendéglátás|
|Gyártás|
|Power & segédprogramok|
|Közbiztonság és nemzetbiztonsági|
|Lakossági & fogyasztási cikkek|
|Szolgáltatások|
|Utazási & szállítás|
|Nagykereskedelmi & eloszlás|

### <a name="solutions"></a>Megoldások

| Érték        |
|-----------------|
|AdvancedAnalytics|
|ApplicationIntegration|
|ArtificialIntelligence|
|AzureSecurityOperationManagement|
    |AzureStack|
    |BackupDisasterRecovery|
    |BigData|
    |Blockchain|
    |Csevegőrobot|
    |CloudDatabaseMigration|
    |CloudMigration|
    |CloudVoice|
    |CognitiveServices|
    |CompetitiveDatabaseMigration|
    |Containers|
    |DataWarehouse|
    |DatabaseonLinux|
    |DevelopmentandTest|
    |DevOps|
    |DigitalMedia|
    |Dynamics365forCustomerService|
    |Dynamics365forFieldService|
    |Dynamics365forFinanceOperations|
    |Dynamics365forRetail|
    |Dynamics365forSales|
    |Dynamics365forTalent|
    |DynamicsonAzure|
    |EnterpriseBusinessIntelligence|
    |Játékok|
    |HighPerformanceComputing|
    |HybridStorage|
    |IdentityandAccessManagement|
    |InformationManagement|
    |InternetofThings|
    |Machine Learning|
    |Microserviceapplications|
    |MobileApplications|
    |MySQLPostgresMigrationtoAzure|
    |Hálózat|
    |NoSQLMigration|
    |RedhatonAzure|
    |RegulatoryComplianceGDPR|
    |SAPonAzure|
    |ServerlessComputing|
    |SharepointonAzure|
    |SQLServerUpgrade|
    |ThreatProtection|
    |Webfejlesztés|

### <a name="customer-size"></a>Ügyfél mérete

| Érték        |
|-----------------|
|    1to50employees|
|    51to500employees|
|    Morethan500employees|
|    1to9employees|
|    10to50employees|
|    51to250employees|
|    251to1000employees|
|    1001to5000employees|
|    5001to10000employees|
|    10001to20000employees|
|    Morethan20000employees|
