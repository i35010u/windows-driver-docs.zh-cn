---
title: wdfkd.wdfusbdevice
description: 所有 USB 接口和配置管道，wdfkd.wdfusbdevice 扩展将显示有关指定 KMDF USB 设备对象，其中包括的信息。
ms.assetid: 94e0a4ef-36a6-4a37-ac4a-5a2ee2678b9a
keywords:
- wdfkd.wdfusbdevice Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfusbdevice
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d83e17bdee8aa1aacae12a6f453856b192904a5c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323305"
---
# <a name="wdfkdwdfusbdevice"></a>!wdfkd.wdfusbdevice


！ Wdfkd.wdfusbdevice 扩展显示有关指定的内核模式驱动程序框架 (KMDF) USB 设备对象的信息。 此信息包括所有 USB 接口以及为每个接口配置的管道。

```dbgcmd
!wdfkd.wdfusbdevice Handle [Flags]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *句柄*   
WDFUSBDEVICE 键入 USB 设备对象的句柄。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
可选。 一个十六进制值，修改要返回的信息的类型。 默认值为 0x0。 标志可以是以下位的任意组合：

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
显示将包括 I/O 目标的属性。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
显示将包括 I/O 目标为每个 USB 管道对象的属性。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架

KMDF 1，UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

 

 





