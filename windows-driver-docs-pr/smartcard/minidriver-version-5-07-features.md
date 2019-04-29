---
title: 微型驱动程序版本 5.07 功能
description: 微型驱动程序版本 5.07 功能
ms.assetid: BFB38805-D2D3-40D2-B336-127B3B84141D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1096273ecc33287e464d7ebc1af71797adc1386
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380215"
---
# <a name="minidriver-version-507-features"></a>微型驱动程序版本 5.07 功能


在此版本中引入以下功能。

## <a name="span-idchangestothecarddatastructurespanspan-idchangestothecarddatastructurespanspan-idchangestothecarddatastructurespanchanges-to-the-carddata-structure"></a><span id="Changes_to_the_CARD_DATA_structure"></span><span id="changes_to_the_card_data_structure"></span><span id="CHANGES_TO_THE_CARD_DATA_STRUCTURE"></span>将更改为卡\_数据结构


[**卡片\_数据**](https://msdn.microsoft.com/library/windows/hardware/dn468748)结构包括以下更改：

-   **Dw 版本**成员，作为输入，被视为所需的版本要从返回[ **CardAcquireContext** ](https://msdn.microsoft.com/library/windows/hardware/dn468701)函数。 较旧卡微型驱动程序可能只支持版本 4 入口点，但是。 所有卡微型驱动程序将都设置版本返回，这是&lt;= 中传递的版本。 现有基本 CSP 的和基于 SC KSP 的卡微型驱动程序将更新为具有，也可以此行为。
-   **PfnCardPrivateKeyDecrypt**替换为成员**pfnCardRSADecrypt**成员。 关联的结构和函数类型已修改以反映这一情况。
-   **PfnCardSign**添加成员。 这将使用仅未填充的输入并将执行基于指定的密钥加密签名。 对于 ECC 卡微型驱动程序，这将是 ECDSA 操作。
-   **PfnCardConstructDHAgreement**添加成员。 这执行 Diffie Helman 密钥协议。 对于 ECC 卡微型驱动程序，这将是 ECDHE 操作。
-   **PfnCspPadData**入口点添加，以便不支持在卡填充的卡可以回调到 CSP/KSP 以填充其数据。

## <a name="span-idexpandedmeaningofthedwkeyspecparameterspanspan-idexpandedmeaningofthedwkeyspecparameterspanspan-idexpandedmeaningofthedwkeyspecparameterspanexpanded-meaning-of-the-dwkeyspec-parameter"></a><span id="Expanded_meaning_of_the_dwKeySpec_parameter"></span><span id="expanded_meaning_of_the_dwkeyspec_parameter"></span><span id="EXPANDED_MEANING_OF_THE_DWKEYSPEC_PARAMETER"></span>这意味着 dwKeySpec 参数的扩展


含义**dwKeySpec**扩展成员或参数 （在各种结构和入口点中存在）。

-   在\_KEYEXCHANGE 和 AT\_签名表示 RSA 密钥和其预期的用途。 RSA 密钥大小的正则的进度。
-   ECC 密钥将有很少的大小，并且不遵循常规的进度。 ECC **dwKeySpec**将指示确切大小，例如 AT\_ECDHA\_P521 ECDHA 曲线 P 521 位密钥。 请参阅[ **CardCreateContainer** ](https://msdn.microsoft.com/library/windows/hardware/dn468708)有关新的完整列表**dwKeySpec**常量。

## <a name="span-idmanifestregistrationspanspan-idmanifestregistrationspanspan-idmanifestregistrationspanmanifest-registration"></a><span id="Manifest_registration"></span><span id="manifest_registration"></span><span id="MANIFEST_REGISTRATION"></span>清单注册


注册已识别卡 ATRs 现在不能与处理清单中，通过*DllRegisterServer*并*DllUnRegisterServer*。

## <a name="span-idinterfacesforsecretagreementchangesspanspan-idinterfacesforsecretagreementchangesspanspan-idinterfacesforsecretagreementchangesspaninterfaces-for-secret-agreement-changes"></a><span id="Interfaces_for_Secret_Agreement_Changes"></span><span id="interfaces_for_secret_agreement_changes"></span><span id="INTERFACES_FOR_SECRET_AGREEMENT_CHANGES"></span>接口的机密协议更改


接口的 ECDH 密钥协议更改进行更新。

 

 





