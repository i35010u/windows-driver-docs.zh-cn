---
title: wdfkd.wdfusbinterface
description: Wdfkd.wdfusbinterface 扩展显示有关指定的内核模式驱动程序框架 (KMDF) USB 接口对象，其中包括其可能和当前设置的信息。
ms.assetid: 2c0788aa-adb0-4a51-9937-32c8d9e0c240
keywords:
- wdfkd.wdfusbinterface Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfusbinterface
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 048d1627bfc40b613da7b859c06b56543a548747
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563140"
---
# <a name="wdfkdwdfusbinterface"></a>!wdfkd.wdfusbinterface


**！ Wdfkd.wdfusbinterface**扩展显示有关指定的内核模式驱动程序框架 (KMDF) USB 接口对象，其中包括其可能和当前设置的信息。

```dbgcmd
!wdfkd.wdfusbinterface Handle [Flags]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *句柄*   
WDFUSBINTERFACE 键入 USB 接口对象的句柄。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
可选。 一个十六进制值，修改要返回的信息的类型。 默认值为 0x0。 标志可以是以下位的任意组合：

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
显示将包括 I/O 目标为每个 KMDF USB 管道对象的属性。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架

KMDF 1，UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

 

 





