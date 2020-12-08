---
title: wdfkd.wdfsetdriver
description: Wdfkd. wdfsetdriver 扩展设置应用调试器扩展命令的默认 Kernel-Mode Driver Framework (KMDF) 驱动程序的名称。
keywords:
- wdfkd wdfsetdriver Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfsetdriver
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9d8d14870200ac6118c4e86200ae33ea05f1408e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837013"
---
# <a name="wdfkdwdfsetdriver"></a>!wdfkd.wdfsetdriver


**！ Wdfkd。 wdfsetdriver** 扩展设置应用调试器扩展命令的默认 Kernel-Mode driver FRAMEWORK (KMDF) 驱动程序的名称。

```dbgcmd
!wdfkd.wdfsetdriver DriverName
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______DriverName______"></span><span id="_______drivername______"></span><span id="_______DRIVERNAME______"></span>*DriverName*   
驱动程序的名称。 *DriverName* 不得包含 .sys 文件扩展名。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作

KMDF 1，UMDF 2

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

**！ Wdfkd. wdfsetdriver** 扩展设置默认的驱动程序名称。 你可以将此名称用于其他 **wdfkd** 扩展，否则将要求你指定驱动程序名称。

若要获取当前默认 KMDF 驱动程序的名称，请使用 [**！ wdfgetdriver**](-wdfkd-wdfgetdriver.md) 扩展。

 

 





