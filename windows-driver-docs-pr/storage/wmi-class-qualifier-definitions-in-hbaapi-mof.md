---
title: Hbaapi.mof 中的 WMI 类限定符定义
description: Hbaapi.mof 中的 WMI 类限定符定义
ms.assetid: 9db543f1-f6ad-4735-8ba0-21476aa229ba
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a03a93846b33159ceabe2760e093927dae4d8393
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330301"
---
# <a name="wmi-class-qualifier-definitions-in-hbaapimof"></a>Hbaapi.mof 中的 WMI 类限定符定义


## <span id="ddk_wmi_class_qualifier_definitions_in_hbaapi_mof_kr"></span><span id="DDK_WMI_CLASS_QUALIFIER_DEFINITIONS_IN_HBAAPI_MOF_KR"></span>


由定义的 WMI 类限定符*Hbaapi.mof*文件如下所示：

[事件\_类型\_限定符](event-types-qualifiers.md)

[HBA\_BIND\_TYPE](hba-bind-type.md)

[HBA\_状态](hba-status.md)

此部分所述的限定符之一到 WMI 类定义，它表示任何组，可以分配该字段中的数据字段的应用时预先确定的限定符中的定义中指示的整数值*Hbaapi.mof*。 因此此处所述的每个 WMI 类限定符类似于一个枚举器，它表示一组整数值，但 WMI 工具套件不会在生成中的枚举器声明*Hbapiwmi.h*对应于中的限定符*Hbaapi.mof*，也不会生成一系列的限定符值相对应的符号常量定义。

但是，通过包括*Hbaapi.h*驱动程序或应用程序可以使用一系列以期提供易于记忆的名称与定义的 WMI 类限定符关联的每个值定义的符号常量在中*Hbaapi.mof*。

有关 WMI 类限定符的一般讨论，请参阅[WMI 类限定符](https://msdn.microsoft.com/library/windows/hardware/ff566348)。

 

 





