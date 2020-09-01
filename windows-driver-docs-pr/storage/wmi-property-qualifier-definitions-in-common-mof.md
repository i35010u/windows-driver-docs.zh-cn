---
title: Common.mof 中的 WMI 属性限定符定义
description: Common.mof 中的 WMI 属性限定符定义
ms.assetid: 24a95c4b-f4f4-4042-9a06-069685ac0260
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1649246e822f782fd9a1a320b0fd730e77dcd22a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191609"
---
# <a name="wmi-property-qualifier-definitions-in-commonmof"></a>Common.mof 中的 WMI 属性限定符定义


## <span id="ddk_wmi_property_qualifier_definitions_in_common_mof_kr"></span><span id="DDK_WMI_PROPERTY_QUALIFIER_DEFINITIONS_IN_COMMON_MOF_KR"></span>


*常见的 mof*文件定义以下 WMI 属性限定符：

[ISCSI \_ 身份验证 \_ 类型 \_ 限定符](iscsi-auth-types-qualifiers.md)

[ISCSI \_ 状态 \_ 限定符](iscsi-status-qualifiers.md)

[安全 \_ 标志 \_ 限定符](security-flag-qualifiers.md)

如果您将上述某个限定符应用于 WMI 类定义中的数据字段，则它表示您可以将在限定符定义中指示的任何整数值分配给相应的结构成员。

因此，WMI 属性限定符类似于枚举，因为限定符表示一组整数值。 但 WMI 工具套件不会在 *Iscsidef* 中生成对应于 *Common*限定符的枚举声明，这两种方法都不会生成与限定符值相对应的一组符号常量定义。

有关 WMI 属性限定符的一般讨论，请参阅 [Wmi 属性限定符](../kernel/wmi-property-qualifiers.md)。

 

