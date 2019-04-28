---
title: wdfkd.wdfwmi
description: Wdfkd.wdfwmi 扩展显示指定的框架设备对象的 Microsoft Windows Management Instrumentation (WMI) 信息。
ms.assetid: fd521be8-3c7a-415b-8044-c9fb25188cbc
keywords:
- wdfkd.wdfwmi Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfwmi
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e38c0934364eac907830fe1dacfcba2b599a4894
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342566"
---
# <a name="wdfkdwdfwmi"></a>!wdfkd.wdfwmi


**！ Wdfkd.wdfwmi**扩展显示指定的框架设备对象的 Microsoft Windows Management Instrumentation (WMI) 信息。 此信息包括所有的 WMI 提供程序对象和其关联的 WMI 实例对象。

```dbgcmd
!wdfkd.wdfwmi Handle
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *句柄*   
Framework 设备对象的句柄。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架

KMDF 1

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

输出 **！ wdfkd.wdfwmi**扩展包括有关 WMI 注册、 提供商和实例的信息。

 

 





