---
title: wdfkd.wdfiotarget
description: Wdfkd.wdfiotarget 扩展显示有关指定的 I/O 目标对象的信息。
ms.assetid: 60a864cc-5099-4d8c-8712-1ba48bce1e0f
keywords:
- wdfkd.wdfiotarget Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfiotarget
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: be901cadae35767aa6a6536502858a39528f3bd4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563520"
---
# <a name="wdfkdwdfiotarget"></a>!wdfkd.wdfiotarget


**！ Wdfkd.wdfiotarget**扩展显示有关指定的 I/O 目标对象的信息。

```dbgcmd
!wdfkd.wdfiotarget Handle [Flags]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *句柄*   
I/O 目标对象的句柄。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
可选。 指定要显示的信息类型的标志。 *标志*可以是以下位的任意组合。 默认值为 0x0。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
显示将包括的每个 I/O 目标的挂起的请求对象的详细信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架

KMDF 1，UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

下面的示例演示从显示器 **！ wdfkd.wdfiotarget**扩展。

```dbgcmd
kd> !wdfiotarget 0x7c9630b8 

# WDFIOTARGET 8369cf40
=========================
WDFDEVICE: 0x7ca7b1c0
Target Device:  !devobj 0x81ede5d8
Target PDO: !devobj 0x822b8a90

Type: Instack target
State:  WdfIoTargetStarted

Requests waiting: 0

Requests sent: 0

Requests sent with ignore-target-state: 0
```

在前面的示例输出包括 I/O 目标的父框架设备对象，以及 WDM 设备的地址的地址\_表示目标驱动程序的设备对象和目标设备的对象结构物理设备对象 (PDO)。

 

 





