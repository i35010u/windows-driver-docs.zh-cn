---
title: wdfkd.wdfumtriage
description: Wdfkd wdfumtriage 扩展显示系统上的信息 UMDF 设备，包括设备对象、加载的驱动程序和类扩展、PnP 设备堆栈、调度的 Irp。
keywords:
- wdfkd wdfumtriage Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfumtriage
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f3a46b6152c8c516a057144545f90da8d141d087
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823613"
---
# <a name="wdfkdwdfumtriage"></a>!wdfkd.wdfumtriage


**！ Wdfkd; wdfumtriage** 扩展显示系统上所有 UMDF 设备的相关信息，包括设备对象、相应的主机进程、已加载的驱动程序和类扩展、PnP 设备堆栈、pnp 设备节点、调度的 irp 以及相关的问题状态。

```dbgcmd
!wdfkd.wdfumtriage
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Wdfkd.dll

## <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作


UMDF 2

## <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息


有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

可以在内核模式调试会话中使用此命令。

下面是 **！ wdfkd** 的输出示例。

![从！ wdfkd. wdfumtriage 的驱动程序对象列表输出](images/wdfumtriage2.png)

 

 





