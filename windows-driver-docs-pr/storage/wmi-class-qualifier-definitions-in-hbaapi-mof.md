---
title: Hbaapi.mof 中的 WMI 类限定符定义
description: Hbaapi.mof 中的 WMI 类限定符定义
ms.assetid: 9db543f1-f6ad-4735-8ba0-21476aa229ba
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2d7df1845fb428b8d0c61063114107b888223421
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191613"
---
# <a name="wmi-class-qualifier-definitions-in-hbaapimof"></a>Hbaapi.mof 中的 WMI 类限定符定义


## <span id="ddk_wmi_class_qualifier_definitions_in_hbaapi_mof_kr"></span><span id="DDK_WMI_CLASS_QUALIFIER_DEFINITIONS_IN_HBAAPI_MOF_KR"></span>


*Hbaapi*文件定义的 WMI 类限定符如下所示：

[事件 \_ 类型 \_ 限定符](event-types-qualifiers.md)

[HBA \_ 绑定 \_ 类型](hba-bind-type.md)

[HBA \_ 状态](hba-status.md)

如果本部分中描述的某个限定符应用于 WMI 类定义中的数据字段，则表示该字段可分配给 *Hbaapi*中的限定符定义中指示的任何预设整数值集。 因此此处所述的每个 WMI 类限定符都类似于一个枚举器，因为它表示一组整数值，但 WMI 工具套件不会在 *Hbapiwmi* 中生成与 *Hbaapi*中的限定符相对应的枚举器声明，也不会生成与限定符值相对应的一组符号常量定义。

但是，通过包含 *Hbaapi* ，你的驱动程序或应用程序可以使用一组符号常量，这些常量用视图定义，以便为与在 *Hbaapi*中定义的 WMI 类限定符关联的每个值提供易于记住的名称。

有关 WMI 类限定符的一般讨论，请参阅 [Wmi 类限定符](../kernel/wmi-class-qualifiers.md)。

 

