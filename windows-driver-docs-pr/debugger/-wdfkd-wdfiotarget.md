---
title: wdfkd.wdfiotarget
description: Wdfkd. wdfiotarget 扩展显示有关指定 i/o 目标对象的信息。
keywords:
- wdfkd wdfiotarget Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfiotarget
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 46309f359fb5c866db41d09742d32fb975a581bf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838389"
---
# <a name="wdfkdwdfiotarget"></a>!wdfkd.wdfiotarget


**！ Wdfkd wdfiotarget** 扩展显示有关指定 i/o 目标对象的信息。

```dbgcmd
!wdfkd.wdfiotarget Handle [Flags]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span>*句柄*   
I/o 目标对象的句柄。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
可选。 用于指定要显示的信息类型的标志。 *标志* 可以是以下位的任意组合。 默认值为0x0。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)   
显示将包括每个 i/o 目标的挂起请求对象的详细信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作

KMDF 1，UMDF 2

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

下面的示例演示了 **！ wdfkd. wdfiotarget** 扩展中的显示。

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

前面的示例中的输出包含 i/o 目标的父框架设备对象的地址，以及 \_ 表示目标驱动程序的设备对象和目标设备的物理设备对象 (PDO) 的 WDM 设备对象结构的地址。

 

 





