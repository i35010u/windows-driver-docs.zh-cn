---
title: 微型驱动程序版本 5.07 功能
description: 微型驱动程序版本 5.07 功能
ms.assetid: BFB38805-D2D3-40D2-B336-127B3B84141D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4482b29619918a7abe355d12cf66d4d1bcfbc22d
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381657"
---
# <a name="minidriver-version-507-features"></a>微型驱动程序版本 5.07 功能


此版本中引入了以下功能。

## <a name="span-idchanges_to_the_card_data_structurespanspan-idchanges_to_the_card_data_structurespanspan-idchanges_to_the_card_data_structurespanchanges-to-the-card_data-structure"></a><span id="Changes_to_the_CARD_DATA_structure"></span><span id="changes_to_the_card_data_structure"></span><span id="CHANGES_TO_THE_CARD_DATA_STRUCTURE"></span>对卡 \_ 数据结构的更改


[**卡 \_数据**](/previous-versions/dn468748(v=vs.85)) 结构更改，包括以下内容：

-   **DwVersion**成员作为输入，作为要从[**CardAcquireContext**](/previous-versions/dn468701(v=vs.85))函数返回的所需版本。 不过，较旧的卡微型驱动程序可能仅支持版本4入口点。 所有卡微型驱动程序将设置返回的版本，即 &lt; 传入的版本。 现有的基本 CSP 和基于 SC KSP 的卡微型驱动程序也将更新为具有此行为。
-   **PfnCardPrivateKeyDecrypt**成员被替换为**pfnCardRSADecrypt**成员。 修改关联的结构和函数类型，以反映此情况。
-   添加了 **pfnCardSign** 成员。 这只需要未填充输入，并将根据所指示的密钥执行加密签名。 对于 ECC 卡微型驱动程序，这将是一个 ECDSA 运算。
-   添加了 **pfnCardConstructDHAgreement** 成员。 这会执行 Helman 密钥协议。 对于 ECC 卡微型驱动程序，这将是一种 ECDHE 操作。
-   添加了 **pfnCspPadData** 入口点，以便不支持卡上填充的卡可以回叫 CSP/KSP，使其数据已填充。

## <a name="span-idexpanded_meaning_of_the_dwkeyspec_parameterspanspan-idexpanded_meaning_of_the_dwkeyspec_parameterspanspan-idexpanded_meaning_of_the_dwkeyspec_parameterspanexpanded-meaning-of-the-dwkeyspec-parameter"></a><span id="Expanded_meaning_of_the_dwKeySpec_parameter"></span><span id="expanded_meaning_of_the_dwkeyspec_parameter"></span><span id="EXPANDED_MEANING_OF_THE_DWKEYSPEC_PARAMETER"></span>DwKeySpec 参数的扩展含义


**DwKeySpec**成员或参数 (在不同结构和入口点中存在的意义) 展开。

-   在 \_ KEYEXCHANGE 和 at \_ 签名指示 RSA 密钥及其预期用途。 RSA 密钥的大小遵循定期进度。
-   ECC 密钥的大小会极少，并且不遵循定期进度。 ECC **dwKeySpec** 将指示确切的大小，例如 \_ ECDHA \_ P521 for ECDHA 的 P 曲线521位键。 请参阅 [**CardCreateContainer**](/previous-versions/dn468708(v=vs.85)) ，以获取新 **dwKeySpec** 常量的完整列表。

## <a name="span-idmanifest_registrationspanspan-idmanifest_registrationspanspan-idmanifest_registrationspanmanifest-registration"></a><span id="Manifest_registration"></span><span id="manifest_registration"></span><span id="MANIFEST_REGISTRATION"></span>清单注册


现在可通过清单（而不是 *DllRegisterServer* 和 *DllUnRegisterServer*）来注册可识别卡的 ATRs。

## <a name="span-idinterfaces_for_secret_agreement_changesspanspan-idinterfaces_for_secret_agreement_changesspanspan-idinterfaces_for_secret_agreement_changesspaninterfaces-for-secret-agreement-changes"></a><span id="Interfaces_for_Secret_Agreement_Changes"></span><span id="interfaces_for_secret_agreement_changes"></span><span id="INTERFACES_FOR_SECRET_AGREEMENT_CHANGES"></span>用于机密协议更改的接口


更新了对 ECDH 的机密协议更改的接口。

 

