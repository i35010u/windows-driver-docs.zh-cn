---
title: Common.mof 中的 WMI 属性限定符定义
description: Common.mof 中的 WMI 属性限定符定义
ms.assetid: 24a95c4b-f4f4-4042-9a06-069685ac0260
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 658c6ffb54e5150d8f3989d6950cb81c246e21d0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386787"
---
# <a name="wmi-property-qualifier-definitions-in-commonmof"></a>Common.mof 中的 WMI 属性限定符定义


## <span id="ddk_wmi_property_qualifier_definitions_in_common_mof_kr"></span><span id="DDK_WMI_PROPERTY_QUALIFIER_DEFINITIONS_IN_COMMON_MOF_KR"></span>


*Common.mof*文件定义以下 WMI 属性限定符：

[ISCSI\_AUTH\_TYPES\_QUALIFIERS](iscsi-auth-types-qualifiers.md)

[ISCSI\_状态\_限定符](iscsi-status-qualifiers.md)

[安全\_标志\_限定符](security-flag-qualifiers.md)

如果您将一个前面的限定符应用于 WMI 类定义中的数据字段时，它表示可分配任何相应的结构成员的限定符的定义中指示的整数值。

因此，WMI 属性限定符类似于一个枚举，因为限定符表示一组整数值。 但 WMI 工具套件不会生成在枚举声明*Iscsidef.h*对应于中的限定符*Common.mof*，它既不会生成一组符号常量定义对应于限定符值。

有关 WMI 属性限定符的一般讨论，请参阅[WMI 属性限定符](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-property-qualifiers)。

 

 





