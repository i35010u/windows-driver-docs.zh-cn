---
title: wdfkd.wdfwmi
description: Wdfkd. wdfwmi 扩展显示特定框架设备对象 (WMI) 信息的 Microsoft Windows Management Instrumentation。
keywords:
- wdfkd wdfwmi Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfwmi
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f62231c6a13a89b9730a382cfa715d0d94b19b11
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823589"
---
# <a name="wdfkdwdfwmi"></a>!wdfkd.wdfwmi


**！ Wdfkd wdfwmi** 扩展显示特定框架设备对象 (WMI) 信息的 Microsoft Windows Management Instrumentation。 此信息包括所有 WMI 提供程序对象及其关联的 WMI 实例对象。

```dbgcmd
!wdfkd.wdfwmi Handle
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span>*句柄*   
框架设备对象的句柄。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作

KMDF 1

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

**！ Wdfkd wdfwmi** 扩展的输出包含有关 WMI 注册、提供程序和实例的信息。

 

 





